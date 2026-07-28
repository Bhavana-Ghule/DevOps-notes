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

After installation generate the key on master node and copy public key and add it into the worker node .ssh/authorized key file inside of it without removing old data <br>
After that copy private ip of worker node and paste into master's /etc/ansible inside of it one hosts file their dd private io of worker node in that<br>
Then run this commad for comfiguration o master's node :-><br>
ANSIBLE_HOST_KEY_CHECKING=False ansible -i /etc/ansible/hosts all -m ping<br>
ansible all -m ping<br>
