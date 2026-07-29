## what is ansible?
Ansible provides open-source automation that reduces complexity and runs everywhere. Using Ansible lets you automate virtually any task.
#### The easiest way to remember is:
Terraform creates the house.<br>
Ansible arranges the furniture, installs appliances, and makes the house ready to live in.

---

## Installing ansible on ubuntu:->
$ sudo apt update<br>
$ sudo apt install software-properties-common<br>
$ sudo add-apt-repository --yes --update ppa:ansible/ansible<br>
$ sudo apt install ansible<br>

##### After installation generate the key on master node and copy public key and add it into the worker node .ssh/authorized key file inside of it without removing old data <br>
##### After that copy private ip of worker node and paste into master's /etc/ansible inside of it one hosts file their dd private io of worker node in that<br>
##### Then run this commad for comfiguration o master's node :-><br>
ANSIBLE_HOST_KEY_CHECKING=False ansible -i /etc/ansible/hosts all -m ping<br>
ansible all -m ping<br>
##### To control the worker node you need to create yaml playbook inside the masternode so you just to run the following command for execute the file 
ansible-playbook playbook.yaml <br>
ansible-playbook playbook.yaml -vv <br>

----

## For installing docker on worker node 
---
- name: Install Docker on Worker Nodes<br>
  hosts: workers<br>
  become: yes<br>
  tasks:<br>
    - name: Update apt packages<br>
      apt:<br>
        update_cache: yes<br>
    - name: Install Docker<br>
      apt:<br>
        name: docker.io<br>
        state: present<br>
    - name: Start Docker Service<br>
      service:<br>
        name: docker<br>
        state: started<br>
    - name: Enable Docker Service<br>
      service:<br>
        name: docker<br>
        enabled: yes<br>

---

##### Understanding Ansible Play Recap States:
when an ansible playbook finished execution, it displays a summary called PLAY RECAP.<br>
Example: <br>
172.31.12.169 : ok-2 changed-1 unreachable-0 failed-0 skipped-0 rescued-0 ignored-0 <br>
This summary helps to find out what happened during playbook execution.

### States:
1. ok = Give task executed successfully
2. changed =Task modified the server
3. unreachable =no. of server was reachable
4. failed = no. of task failed
5. skipped = no. of task was skipped
6. rescued = no. of task was recovered
7. ignored = no. of errors were ignored

### Interview Questions:
##### What is Ansible?
It is an opensource automation and configuration management tool used for server provisioning, application deployment, and orchestration.
