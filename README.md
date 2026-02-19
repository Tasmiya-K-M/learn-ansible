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

1. How ansible connects to the node? 
    ansible uses SSH
    ansible needs inventory

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

6. order of task doesn't matter in ansible-playbook


