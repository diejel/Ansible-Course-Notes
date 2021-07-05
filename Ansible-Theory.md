Ansible-Installation
------------------------
Centos:
sudo yum install  epel-release
sudo yum install ansible
ansible --version


Debian:
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list

sudo apt install -y dirmngr

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

sudo apt update

sudo apt install -y ansible sshpass 

Configuration Hierarchy
-----------------------
Environmental Variable: ANSIBLE_CONFIG
ansible.cfg  in Working Directory
$HOME/.ansible.cfg
/etc/ansible/ansible.cfg


ansible --version -> Show config file

echo > ~/.ansible.cfg

Show current file contents
========================
> ansible-config view

Show all configuration
=======================
> ansible-config list

Show current settings
======================
> ansible-config dump

Show only non-default settings
=============================
> ansible-config dump --only-changed

Sample of configuratio file
===========================
[defaults]
inventory=inventory ; set inventory file in the same working directory

remote_user = tux

#Full comments

[privilege_escalation]
become = true; or set in play when needed
become_method = sudo
########################
#Ansible Inventory
This is a list of hosts,groups and variables that normally or
by default is in /etc/ansible/hosts.

Example of an inventory file
----------------------------

192.168.56.2 ansible_connection=local

[webservers]
192.168.56.[2:4]

[ubuntu]
192.168.56.4

[centos]
192.168.56.[2:3]

[uk:children]
centos
ubuntu

#####################

Query INventory
---------------
This is the way how you make request to query
for listing hosts in your inventory file

* If you ommit -i , you will look up in the inventory
file configured

$ ansible -i hosts --lists-hosts ubuntu

$ ansible -i hosts --list-hosts webservers

Separate HOsts and Varibales
----------------------------
Is a better practice to separate hosts and groups in differnet
folders for example "host_vars, group_vars" groups.

$ mkdir ./host_vars
$ echo "ansible_connection: local" > host_vars/192.168.56.2


###################
Ad-hoc commands
----------------
-m -> to reference the ansible module
-a -> to reference optional arguments to module
-i -> to reference a different inventory
-k -> to prompt for ssh password

* Basic Configuration
----------------------
From inventory hosts we will perform a simple script for
scan the publick ssh key cached  and add it to known_hosts file and
be accepted when we try to establish a secure communication

$ for h in 192.168.56.{2..4}; do ssh-keyscan $h >> ~/.ssh/known_hosts ; done

$ ssh-keygen (for generation)

*  Ping Hosts
---------------
This is not related to ICMP protocol, it is called like that but really
this is a module that look for a python interpreter active in the remote hosts
(-k , to prompt ssh password; -K to prompt for SUDO password)

$ ansible all -k -K -m ping 

* Distribute SSH Key
------------------
Distribution of the ssh key in all nodes where is created the same user tux
, add the ssh key in authorized_keys file
 
$ ansible all -k -K -m authorized_key \
-a " user='tux' state='present' \ 
key='{{ lookup('file','/home/tux/.ssh/id_rsa.pub') }}'  "

Copy Sudoers Files
---------------------
To allow passwordless for not being asked everytime for sudo rights

$ echo " tux ALL=(root) NOPASSWD:ALL" > tux
 
To verify if syntax is correct, do:

$ sudo visudo -cf tux

Copy process for all inventory hosts using -b to become sudo and elevate
prvileges using -K, using copy module (-m) and specify the -a argument "..."...

$ ansible all -b -K -m copy -a "src=tux dest=/etc/sudoers.d/tux"

Help on Modules
----------------
list module with ansible-doc -l command.

ansible-doc -l
ansible-doc -l | grep ping
ansible-doc user

Creating Users
-----------------
With user module ,is nedded to specify at least 01 user name as argument.
Must be run as root including the -b option (to become user = root)
You can delete the user with : state=absent

$ ansible  192.168.56.2 -b -m user -a "name=fred"

To delete a user:
$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent"
$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent remove=true"

####################################
Managing SSH Keys using Ansible
###################################

You must run the following code to add the public keys
of your remote hosts to your known_hosts file

$ for h in 192.168.56.{2..4}; do ssh-keyscan $h >> ~/.ssh/known_hosts ; done

Now is needed generate a SSH Key and distribute to our clients
in order we are not asked for entering password at everiy ssh connection.

$ssh-keygen (leave all by default)

After that, now is needed to verify if nodes in your 
inventory has active a python interpreter using the ping module

$ ansible all -k -K -m ping

* remember that you dont have to have any file indicating the ip
and ansib;e_connection=local

After any hosts responds to ping module with success, you need
to distribute your ssh key to the authorized_key file.

$ ansible all -k -K -m authorized_key -a " user='tux' state='present' key='{{ lookup('file','/home/tux/.ssh/id_rsa_ansible.pub')  }}'   "

## Create the user file for be added to sudoers.d folder in our managed hosts
`$ echo " tux ALL=(root) NOPASSWD: ALL  > tux"`

### You can verify the syntax with :
`sudo visudo -cf tux`

### Now, transfer this file to your managed nodes 
`$ ansible all -b -K -m copy -a " src='tux' dest='/etc/sudoers.d/tux'  "`

In this case, `all` means will be trasferred to all host in our inventory.
`-b` is used because will 'become' sudo, due to `-K` specified.
There is no needed anymore `-k` because we have already trasnferred our ssh public key to `authorized_keys` and prompt ssh password is not nedded.
`-m` is used to specify the `copy` module.
Finally `-a` is used for specify the other attributes enclosed by `""`.

If you try to run the previous command without -K ( sudo privilege ), will work too because we have already create the tux user file in sudoers.d directory

### Listing Ansible Documentation Modules  ###
`$ ansible-doc -l`
`$ ansible-doc user` -> For viewing about user module documentation
I you want to view 'Examples', just type `\EXAMPLE`, and inside the response it will redirect the Example section. 

### Playbooks ###
 - Single tab != single white-space
 - You can make vim as a valid yaml editor (~/.vimrc)
 
#### Comapring Tab to Spaces
- 8 spaces = 1 tab (With standard tab setting)
- `:set list` , helps to view that 
    - 8 spaces in vim
    - `^I` 1 tab in vim with standard tab setting

### Sample of vimrc file
- For yaml file we set 
  * Auto indent
  * Expand Tabs to spaces
  * Tab Stop to 02 spaces
  * Shift Width to 02 spaces using auto-indent
  * Column Highlighting ad underlying.

- First line of the vimrc file
    `autocmd FileType yaml setlocal ai et ts=2 sw=2 cuc cul`
- Setting the vimrc file
    ```set bg=dark
       autocmd Filetype yaml setlocal ai et ts=2 sw=2 cuc cul
     ```
### Sample of PLaybook ####
- Contains a list of plays 
- A play contians -> list of tasks
- A task contains -> Ansible module with keys and values
O playbook must be located in the same folder of inventory.
```
---

- name: Play 1
  hosts: all
  tasks:
     - name: task 1
       debug:
         msg: "here we are"

```
- Optionally you can check the syntax by doing : ` $ ansible-playbook sample.yml --syntax-check `
- Just execute: ` $ ansible-playbook sample.yml`

### Using variables in Playbooks ###













 