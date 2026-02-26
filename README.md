<!-- configuration management tool -->
Tools that helps in making OS level changes with much more advanced features are tools considered under configuration management tool.
        1. CFEngine
        2. Puppet
        3. Chef
        4. Ansible 
            Ansible solves shell problems
                1. ansible is declarative(do this). 
                2. ansible is hetrogeneous by default(it will work on other OS).
                3. ansible can scale to large infrastructure.

<!-- ANSIBLE -->
Ansible supports both push and pull, we need to understand what works for us better and we need to choose one or both according to our requirements.

AGENTLESS:-
Ansible is Agentless means no need to install any other softwares in worker node to work with ansible master

CONNECTIVITY:-
worker node using below method
    1. Linux -> uses SSH
    2. Windows -> uses Powershell Remoting


INVENTORY:-
    1. Inventory file - information of target worker nodes stored in inventory file.
    2. If you don't create new inventory file, ansible uses default inv file (/etc/ansible/hosts)
    3. Inventory file uses INI Format
    4. Inventory file Parameters:
        ansible_connection - ssh/winrm/localhost
        ansible_port - 22/5986
        ansible_user - root/admin
        ansible_ssh_pass - Password
        eg: web ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_password=Pass
            web - is the alias for host
    5. Different Inventory file format:- INI and YAML.

GROUPING AND PARENT-CHILD RELATIONSHIP:-
    1. Group - Collection of hosts
    2. Child group - Group inside another group
    3. Parent group - Group that contains other groups

    INI Format with Parent–Child
    [webservers]
    web1.example.com
    web2.example.com
    [dbservers]
    db1.example.com
    [production:children]
    webservers
    dbservers

    YAML Inventory Format
    all:
    children:
        production:
        children:
            webservers:
            hosts:
                web1.example.com:
                web2.example.com:
            dbservers:
            hosts:
                db1.example.com:

VARIABLES:-
    Stores information that vareis with each host
    
    variables in inventory:
        eg: web ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_password=Pass

    variables in playbook:
        - name: Print a message
          hosts: localhost
          vars:
            greeting: "Hello from Ansible!"
          tasks:
            - name: Display variable
              debug:
                msg: "{{ greeting }}"

    variables file:
        variable1: value1
        variable2: value2

    we can fetch the variables from inventory file into playbook
        eg: -   name: Set firewall config                        #playbook
                hosts: web
                tasks:
                    - firewalld: 
                        service: https
                        permanent: true
                        state: enabled
                    - firewalld: 
                        service: "{{http_port}}"/tcp
                        permanent: true
                        state: disabled
                    - firewalld: 
                        service: "{{snmp_port}}"/udp
                        permanent: true
                        state: disabled
                    - firewalld: 
                        service: "{{inter_ip_range}}"/24
                        Zone: internal
                        state: enabled


            web http_port=8081 snmp_port=161-162 inter_ip_range=192.0.2.0       #inventory file variables


    variables type:
        1. string  -  username: "admin"
        2. Number   - max_connections: 100
        3. boolean  - debug_mode: 
        4. list variables
        5.  Dictionary variables




1. How ansible connects to the node? 
    ansible uses SSH
    ansible needs inventory (information of target worker nodes stored in inventory file)

ping other server from ansible server using user and password
    for single node --> ansible -i private_ip, all -m ping -e ansible_user=user -e ansible_password=password (all groups)
    for multiple nodes --> ansible -i /tmp/inv all -m ping -e ansible_user=user -e ansible_password=password
    for specific group --> ansible -i /tmp/inv group_name -m ping -e ansible_user=user -e ansible_password=password

2. How ansible manages the node configuration?
    Earlier Modules , latest Collections(group of module) 

3. How ansible handles ?
    Install Collections, File Collections, Service Collections ----> Ansible playbook

4. Plain, list , map/dictionary in yaml
    a: 10 --> Plain
    b: [ 99, 89 ] --> list
    b:            --> list
     - 99
     - 89
    c:            --> dict
       course: Devops
       time: 730am
    c: { course: Devops; time: 730am}. --> dict

5. Ansible playbook has list of plays, the play must have tasks or roles

6. order of task doesn't matter in ansible-playbook (Declarative)

7. Run ansible playbook
    ansible-playbook -i private_ip, -e ansible_user=username -e ansible_password=password frontend.yml (push machanism - we will run on master node)

8. ansible-pull -i localhost, -U repo_url  frontend.yml (pull machanism - we will run on worker nodes and ansible should be there) 

9. load yml file in playbook

10. declare variables in playbook

11. roles are used to organize and reuse automation code in a clean, structured way.








