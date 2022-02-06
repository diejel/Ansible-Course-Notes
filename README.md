# 1. Ansible Notes

- [1. Ansible Notes](#1-ansible-notes)
  - [1.1. Menu](#11-menu)
    - [1.1.1. Ansible-Installation](#111-ansible-installation)
    - [1.1.2. Configuration Hierarchy](#112-configuration-hierarchy)
    - [1.1.3. **Securing ANSIBLE_CONFIG Variable**](#113-securing-ansible_config-variable)
    - [1.1.4. Show current file contents](#114-show-current-file-contents)
    - [1.1.5. Show all configuration](#115-show-all-configuration)
    - [1.1.6. Show current settings](#116-show-current-settings)
    - [1.1.7. Show only non-default settings](#117-show-only-non-default-settings)
  - [1.2. Sample of configuration file](#12-sample-of-configuration-file)
  - [1.3. Ansible Inventory](#13-ansible-inventory)
    - [1.3.1. Example of an inventory file](#131-example-of-an-inventory-file)
    - [1.3.2. Perform a quickly search and creae an Inventory](#132-perform-a-quickly-search-and-creae-an-inventory)
    - [1.3.3. Query Inventory](#133-query-inventory)
    - [1.3.4. Separate Hosts and Variables](#134-separate-hosts-and-variables)
    - [1.3.5. Ad-hoc commands](#135-ad-hoc-commands)
    - [1.3.6. Basic Configuration](#136-basic-configuration)
    - [1.3.7. Ping Hosts](#137-ping-hosts)
    - [1.3.8. Distribute SSH Key](#138-distribute-ssh-key)
    - [1.3.9. Copy Sudoers Files](#139-copy-sudoers-files)
    - [1.3.10. **In case we have a Vagrant environment deployment**](#1310-in-case-we-have-a-vagrant-environment-deployment)
    - [1.3.11. Vagrant SSH Keys](#1311-vagrant-ssh-keys)
    - [1.3.12. Help on Modules](#1312-help-on-modules)
  - [1.4. Creating Users](#14-creating-users)
  - [1.5. Managing SSH Keys using Ansible](#15-managing-ssh-keys-using-ansible)
  - [1.6. Create the user file for be added to sudoers.d folder in our managed hosts](#16-create-the-user-file-for-be-added-to-sudoersd-folder-in-our-managed-hosts)
    - [1.6.1. You can verify the syntax with :](#161-you-can-verify-the-syntax-with-)
    - [1.6.2. Now, transfer this file to your managed nodes ###](#162-now-transfer-this-file-to-your-managed-nodes-)
    - [1.6.3. Creating User Account](#163-creating-user-account)
    - [1.6.4. Listing Ansible Documentation Modules](#164-listing-ansible-documentation-modules)
    - [1.6.5. Playbooks](#165-playbooks)
    - [1.6.6. Comapring Tab to Spaces](#166-comapring-tab-to-spaces)
    - [1.6.7. Sample of vimrc file](#167-sample-of-vimrc-file)
    - [1.6.8. Sample how to format .nanorc file](#168-sample-how-to-format-nanorc-file)
    - [1.6.9. Sample of PLaybook](#169-sample-of-playbook)
    - [1.6.10. Using variables in Playbooks](#1610-using-variables-in-playbooks)
  - [1.7. Playbook Summary](#17-playbook-summary)
    - [1.7.1. Understanding why use/not use "gather facts"](#171-understanding-why-usenot-use-gather-facts)
  - [1.8. Creating Users](#18-creating-users)
    - [1.8.1. Simplest User Creation](#181-simplest-user-creation)
    - [1.8.2. Simplest User Deletion](#182-simplest-user-deletion)
    - [1.8.3. Create Multiple Users](#183-create-multiple-users)
    - [1.8.4. Create User (Example) [create_user_jodi.yml]](#184-create-user-example-create_user_jodiyml)
    - [1.8.5. Delete User (Example) [delete_user_jodi.yml]](#185-delete-user-example-delete_user_jodiyml)
    - [1.8.6. Create Multiple User (Example) [create_multiple_user.yml]](#186-create-multiple-user-example-create_multiple_useryml)
    - [1.8.7. Delete Multiple User (Example) [delete_multiple_user.yml]](#187-delete-multiple-user-example-delete_multiple_useryml)
    - [1.8.8. Create User Using Variable Substitution (Example) [create_user_variable_substitution.yml]](#188-create-user-using-variable-substitution-example-create_user_variable_substitutionyml)
  - [1.9. User Passwords](#19-user-passwords)
    - [1.9.1. Example of script in Python3](#191-example-of-script-in-python3)
  - [1.10. Create Ansible User](#110-create-ansible-user)
    - [1.10.1. Create identical remote users for ansible](#1101-create-identical-remote-users-for-ansible)
    - [1.10.2. Task to add _sudo_ access](#1102-task-to-add-sudo-access)
    - [1.10.3. Adding your local SSH Key](#1103-adding-your-local-ssh-key)
    - [1.10.4. Creating the devops account](#1104-creating-the-devops-account)
    - [1.10.5. Ad-hoc command to create user account in every inventory hosts](#1105-ad-hoc-command-to-create-user-account-in-every-inventory-hosts)
    - [1.10.6. Allowing Passwordless Sudo Access for `ansible` user](#1106-allowing-passwordless-sudo-access-for-ansible-user)
    - [1.10.7. SSH Key authentication](#1107-ssh-key-authentication)
  - [1.11. Install Multiple Package with Playbook](#111-install-multiple-package-with-playbook)
  - [1.12. Working with Variables and Facts](#112-working-with-variables-and-facts)
    - [1.12.1. Using Multiple Plays](#1121-using-multiple-plays)
    - [1.12.2. Using Facts](#1122-using-facts)
    - [1.12.3. Consider Inventory Variables](#1123-consider-inventory-variables)
    - [1.12.4. Playbook using variables "Admin Groups"](#1124-playbook-using-variables-admin-groups)
    - [1.12.5. Playbook Using Variables "Package MOdule"](#1125-playbook-using-variables-package-module)
  - [1.13. Lab Time!](#113-lab-time)
    - [1.13.1. Installing Apache (Multiple Plays)](#1131-installing-apache-multiple-plays)
    - [1.13.2. Installing Apache ( Logic )](#1132-installing-apache--logic-)
    - [1.13.3. Installing Apache ( Variables)](#1133-installing-apache--variables)

## 1.1. Menu

### 1.1.1. Ansible-Installation ###

Centos:

`sudo yum install  epel-release`

`sudo yum install ansible`

`ansible --version`

Debian:

`echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list`

`sudo apt install -y dirmngr`

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367`

`sudo apt update`

`sudo apt install -y ansible sshpass` 

  - Ubuntu (20.04)
    - `$ sudo apt-add-repository  --yes --update ppa:ansible/ansible`
    
    - `$ sudo apt install ansible`

RHEL:

Enabling Ansible on RHEL 8

- _*Remember* register before your RHEL machine:_
  - ```  
     [vagrant@rhel8 ~]$ sudo subscription-manager register \
      > --username user --password pass --auto-attach
      Registering to: subscription.rhsm.redhat.com:443/subscription
      The system has been registered with ID: xxxxxx-xxxxxx-xxxxx-xxxxxx
      The registered system name is: rhel8
      Installed Product Current Status:
      Product Name: Red Hat Enterprise Linux for x86_64
      Status:       Subscribed


      WARNING

      The yum/dnf plugins: /etc/dnf/plugins/subscription-manager.conf were automatically enabled for the benefit of Red Hat Subscription Management. If not desired, use "subscription-manager config --rhsm.auto_enable_yum_plugins=0" to block this behavior.

  

Next, lookup for an Ansible version

```
  [vagrant@rhel8 ~]$ sudo subscription-manager repos --list | grep ansible | nl
     1	Repo ID:   ansible-2-for-rhel-8-x86_64-source-rpms
     2	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2/source/SRPMS
     3	Repo ID:   ansible-2.8-for-rhel-8-x86_64-source-rpms
     4	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.8/source/SRPMS
     5	Repo ID:   ansible-2.9-for-rhel-8-x86_64-rpms
     6	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.9/os
     7	Repo ID:   ansible-automation-platform-2.1-for-rhel-8-x86_64-rpms
     8	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.1/os
     9	Repo ID:   ansible-2.9-for-rhel-8-x86_64-debug-rpms
    10	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.9/debug
    11	Repo ID:   ansible-automation-platform-2.0-early-access-for-rhel-8-x86_64-rpms
    12	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.0/os
    13	Repo ID:   ansible-2-for-rhel-8-x86_64-rpms
    14	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2/os
    15	Repo ID:   ansible-automation-platform-2.1-for-rhel-8-x86_64-debug-rpms
    16	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.1/debug
    17	Repo ID:   ansible-automation-platform-2.1-for-rhel-8-x86_64-source-rpms
    18	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.1/source/SRPMS
    19	Repo ID:   ansible-automation-platform-2.0-early-access-for-rhel-8-x86_64-source-rpms
    20	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.0/source/SRPMS
    21	Repo ID:   ansible-2.8-for-rhel-8-x86_64-debug-rpms
    22	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.8/debug
    23	Repo ID:   ansible-2.8-for-rhel-8-x86_64-rpms
    24	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.8/os
    25	Repo ID:   ansible-2.9-for-rhel-8-x86_64-source-rpms
    26	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2.9/source/SRPMS
    27	Repo ID:   ansible-automation-platform-2.0-early-access-for-rhel-8-x86_64-debug-rpms
    28	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible-automation-platform/2.0/debug
    29	Repo ID:   ansible-2-for-rhel-8-x86_64-debug-rpms
    30	Repo URL:  https://cdn.redhat.com/content/dist/layered/rhel8/x86_64/ansible/2/debug

```
From results above, we will use the (5) option

`$ sudo subscription-manager --enable ansible-2.9-for-rhel-8-x86_64-rpms`

```
[vagrant@rhel8 ~]$ sudo subscription-manager repos --enable ansible-2.9-for-rhel-8-x86_64-rpms
Repository 'ansible-2.9-for-rhel-8-x86_64-rpms' is enabled for this system.

```

To assure you're using you RHEL repository, and not EPEL repository, disable them.

```
$ sudo yum install -y dnf-plugins-core 
$ sudo yum config-manager --disable epel epel-modular

```

Now, feel free to install Ansible being sure that will obtain from RHEL repository.

`$ sudo yum install ansible -y`

### 1.1.2. Configuration Hierarchy ###
Environmental Variable: `ANSIBLE_CONFIG`

ansible.cfg  in Working Directory

`$HOME/.ansible.cfg`

`/etc/ansible/ansible.cfg`

`$ ansible --version` -> Show config file

`echo > ~/.ansible.cfg`

### 1.1.3. **Securing ANSIBLE_CONFIG Variable** ###

You can make this a Read-Only variable by performing within .bashrc file

`$ declare -xr ANSIBLE_CONFIG=/etc/ansible/ansible.cfg`

In that way, any bad actor who tries to modify variable won`t be able to. 

### 1.1.4. Show current file contents ###

`$ ansible-config view`

### 1.1.5. Show all configuration ###
`$ ansible-config list`

### 1.1.6. Show current settings ###
`$ ansible-config dump`

### 1.1.7. Show only non-default settings ###
It shows what was has changed from reference main config file

`$ ansible-config dump --only-changed`

```
[vagrant@rhel8 ~]$ ansible-config dump --only-changed
DEFAULT_BECOME(/home/vagrant/.ansible.cfg) = True
DEFAULT_HOST_LIST(/home/vagrant/.ansible.cfg) = ['/home/vagrant/inventory']
DEFAULT_REMOTE_USER(/home/vagrant/.ansible.cfg) = tux

```
## 1.2. Sample of configuration file ##
```
[defaults]
inventory=inventory ; set inventory file in the same working directory

remote_user = tux

[privilege_escalation]
become = true; or set in play when needed
become_method = sudo

```

## 1.3. Ansible Inventory ##
This is a list of hosts,groups and variables that normally or
by default is in `/etc/ansible/hosts`.

### 1.3.1. Example of an inventory file ###
```

[webservers]
192.168.56.[2:4]

[ubuntu]
192.168.56.4

[centos]
192.168.56.[2:3]

[uk:children]
centos
ubuntu
```

### 1.3.2. Perform a quickly search and creae an Inventory ###

In this case we can use Nmap package in order to perform a deep and quick search of hosts within the network

you can install nmap for Centos based:

`$ yum install nmap`

- The following command will perform a search for a target port 22 within a 192.168.56.0/24 network.
- P: ping scan, Pn: not perform a ping-scan, p: target port, n: network.

`$ sudo namp -Pn -p22 -n 192.168.56.0/24 --open`

```
[vagrant@rhel8 ~]$ sudo nmap -Pn -p22 -n 192.168.56.0/24 --open
Starting Nmap 7.70 ( https://nmap.org ) at 2021-12-19 10:02 UTC
Nmap scan report for 192.168.56.1
Host is up (0.00037s latency).

PORT   STATE    SERVICE
22/tcp filtered ssh
MAC Address: 0A:00:27:00:00:00 (Unknown)

Nmap scan report for 192.168.56.12
Host is up (0.00036s latency).

PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 08:00:27:5B:1F:99 (Oracle VirtualBox virtual NIC)

Nmap scan report for 192.168.56.13
Host is up (0.00062s latency).

PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 08:00:27:09:FF:36 (Oracle VirtualBox virtual NIC)

Nmap scan report for 192.168.56.100
Host is up (-0.089s latency).

PORT   STATE    SERVICE
22/tcp filtered ssh
MAC Address: 08:00:27:A4:63:D5 (Oracle VirtualBox virtual NIC)

Nmap scan report for 192.168.56.11
Host is up (0.00012s latency).

PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 256 IP addresses (5 hosts up) scanned in 12.66 seconds

```

If we need to output in a greppabl format , add the `--oG` param, and a final `-` to export to sdout

`sudo nmap -Pn -p22 -n 192.168.56.0/24 --open -oG - `

We will use some _awk_ params for customizing our results

` sudo nmap -Pn -p22 -n 192.168.56.0/24 --open -oG - | awk '/22\/open/ { print $2 }' `

### 1.3.3. Query Inventory ###
This is the way how you make request to query
for listing hosts in your inventory file

* If you ommit `-i` , you will look up in the inventory
file configured and if you have another inventory file Ex: "inventory_new", you must include `-i`

`$ ansible -i inventory_new --lists-hosts ubuntu`

`$ ansible  --list-hosts webservers`

### 1.3.4. Separate Hosts and Variables ###
Is a better practice to separate hosts and groups in differnet
folders for example "`host_vars`, `group_vars`" groups.

`$ mkdir ./host_vars`

`$ echo "ansible_connection: local" > host_vars/192.168.56.2`

### 1.3.5. Ad-hoc commands ###

Are performed from the command line , ansible must target nodes and reference a python module.

Example: `$ ansible_connection=local   ansible    localhost   -m  ping `

            |__ optional variable__|   |_ cmd_|  |_ target _|  |_module _|

Example: Installation of zsh 

`$ ansible_connection=local ansible localhost -b -m package -a 'name=zsh' `

  ```
  [vagrant@rhel8 ~]$ ansible_connection=local ansible localhost -b -m package -a 'name=zsh'
  localhost | CHANGED => {
      "changed": true,
      "msg": "",
      "rc": 0,
      "results": [
          "Installed: zsh-5.5.1-6.el8_1.2.x86_64"
      ]
  }

  ```
If you would like to remove the above package:

  - `$ ansible_connection=local ansible localhost -b -m package -a 'name=zsh state=absent' `
  
Some definitions of arguments:

`-m` -> to reference the ansible module

`-a` -> to reference optional arguments to module

`-i` -> to reference a different inventory

`-k` -> to prompt for ssh password

`-K` -> to prompt for SUDO password

`-b` -> to elevate privileges

### 1.3.6. Basic Configuration ###
From inventory hosts we will perform a simple script for
scan the publick ssh key cached  and add it to known_hosts file and
be accepted when we try to establish a secure communication

`$ for h in 192.168.56.{2..4}; do ssh-keyscan $h >> ~/.ssh/known_hosts ; done`

`$ ssh-keygen` (for generation)

### 1.3.7. Ping Hosts ###
This is not related to ICMP protocol, it is called like that but really
this is a module that look for a python interpreter active in the remote hosts
(`-k` , to prompt ssh password; `-K` to prompt for SUDO password)

`$ ansible all -k -K -m ping` 

###  1.3.8. Distribute SSH Key ###
Distribution of the ssh key in all nodes where is created the same user tux
, add the ssh key in authorized_keys file
 
```
$ ansible all -k -K -m authorized_key \
-a " user='tux' state='present' \ 
key='{{ lookup('file','/home/tux/.ssh/id_rsa.pub') }}'  "

```

### 1.3.9. Copy Sudoers Files ###
To allow passwordless for not being asked everytime for sudo rights

`$ echo "tux ALL=(root) NOPASSWD:ALL" > tux`
 
To verify if syntax is correct, do:

`$ sudo visudo -cf tux`

Copy process for all inventory hosts using `-b` to become sudo and elevate
prvileges using `-K`, using copy module `-m` and specify the `-a` argument "..."...

`$ ansible all -b -K -m copy -a "src=tux dest=/etc/sudoers.d/tux"`

- In vagrant scenario:

### 1.3.10. **In case we have a Vagrant environment deployment** ###

- We must copy vagrant keys to our controller node
- Connect to nodes in order to test and collect node public keys
- Create a user with sudo rights (wheel or sudo group) 
- Key generation for vagrant in order to log in as "known" on remote nodes and distribution of this key to nodes.
- Adjust config for using private key.
  
### 1.3.11. Vagrant SSH Keys ###

By default, ssh password authentication is disabled. Each time the system boots new keys are generated. Suppose that our scenario has 02 client nodes,  will be setup for those nodes so they could copy and update its keys into the controller.

SSH configuration in the vagrant server node can be verified as follows

`[user@vagrant-server]$ vagrant ssh-config <node_name>`


  ``` 
  [user@vagrant-server]$ vagrant ssh-config ubuntu
  Host ubuntu
  HostName 127.0.0.1
  User vagrant
  Port 2201
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/user/.vagrant/machines/ubuntu/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

```

If we copy this node`s private key to our controller(rhel8), we can use it to authenticate as a vagrant account on our stream or ubuntu system.

- The following command for scp plugin installation.

`[user@vagrant-server]$ vagrant plugin install vagrant-scp`

- The following command allows copy node private key to the controller node.
  
`[user@vagrant-server]$ vagrant scp <path_private_node_key> <controller_name>:name.key`

- In this scenario we have 01 controller "rhel8"

  - 01 ubuntu node client
  - 01 stream node client

Installation process:


```

user@host > vagrant plugin install vagrant-scp
Installing the 'vagrant-scp' plugin. This can take a few minutes...
Fetching: vagrant-libvirt-0.7.0.gem (100%)
Fetching: vagrant-scp-0.5.9.gem (100%)
Successfully uninstalled vagrant-libvirt-0.7.0
Installed the plugin 'vagrant-scp (0.5.9)'!

```

Copying process:

- First, will be listed all ssh node`s properties
- Second, will be copied client node`s private keys to controller node.


```

user@host > vagrant ssh-config
Host rhel8
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/user/Ansible_Lab/.vagrant/machines/rhel8/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

Host stream
  HostName 127.0.0.1
  User vagrant
  Port 2200
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/user/Ansible_Lab/.vagrant/machines/stream/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

Host ubuntu
  HostName 127.0.0.1
  User vagrant
  Port 2201
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/user/Ansible_Lab/.vagrant/machines/ubuntu/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

```

```
user@host Ansible_Lab> vagrant scp /home/user/Ansible_Lab/.vagrant/machines/stream/virtualbox/private_key rhel8:stream.key
Warning: Permanently added '[127.0.0.1]:2222' (RSA) to the list of known hosts.
private_key                                                                                                                                                 100% 1675     1.5MB/s   00:00    
user@host Ansible_Lab> vagrant scp /home/user/Ansible_Lab/.vagrant/machines/ubuntu/virtualbox/private_key rhel8:ubuntu.key
Warning: Permanently added '[127.0.0.1]:2222' (RSA) to the list of known hosts.
private_key                                                                             


```

Verification process

---
Is performed a listing command for view the private keys on controller.

```
[vagrant@rhel8 ~]$ ls -alsh
total 32K
   0 drwx------. 6 vagrant vagrant  227 Feb  6 16:55 .
   0 drwxr-xr-x. 3 root    root      21 Feb  2 01:22 ..
   0 drwx------. 4 vagrant vagrant   27 Feb  6 02:56 .ansible
4.0K -rw-------. 1 vagrant vagrant   50 Feb  6 02:02 .bash_history
4.0K -rw-r--r--. 1 vagrant vagrant   18 Jul 26  2021 .bash_logout
4.0K -rw-r--r--. 1 vagrant vagrant  141 Jul 26  2021 .bash_profile
4.0K -rw-r--r--. 1 vagrant vagrant  376 Jul 26  2021 .bashrc
4.0K -rw-rw-r--. 1 vagrant vagrant   55 Feb  6 02:42 .gitconfig
   0 drwx------. 2 vagrant vagrant   80 Feb  6 01:54 .ssh
   0 drwxrwxr-x. 5 vagrant vagrant  208 Feb  6 02:01 .vscode-server
4.0K -rw-rw-r--. 1 vagrant vagrant  183 Feb  6 02:01 .wget-hsts
   0 drwxrwxr-x. 3 vagrant vagrant   34 Feb  6 01:54 lab_ansible_pl
4.0K -rw-------. 1 vagrant vagrant 1.7K Feb  6 16:55 stream.key
4.0K -rw-------. 1 vagrant vagrant 1.7K Feb  6 16:54 ubuntu.key

```

Now, from the controller will attempt to connect to our node client`s using the private key.

`user@host > ssh -i <private_key_file> <target_node> `

Be aware that by the first time, will appears a message like below and we have to add by typing "yes":

```

The authenticity of host 'A.B.C.D (A.B.C.D)' can't be established.
ECDSA key fingerprint is SHA256:LBMCbc20y4j6I9XVddhCOk5m4hoyBaPJVBiCbcRz9X8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'A.B.C.D' (ECDSA) to the list of known hosts.

```

- From controller to ubuntu node client:

```

[vagrant@rhel8 ~]$ ssh -i ubuntu.key 192.168.56.13
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

 

Last login: Sun Dec  5 20:45:20 2021 from 10.0.2.2
vagrant@ubuntu:~$ 


```

- From controller to stream node client:


```

[vagrant@rhel8 ~]$ ssh -i stream.key 192.168.56.12
Last login: Sun Dec 19 14:37:43 2021 from 192.168.56.11
[vagrant@stream ~]$ 


```

- Now, will be performed a " _ping_ " test. Remember that this ping test is not an ICMP test. this is a test to know if the client node has a python interpreter. In the following example will be specified a username _vagrant_ , the module _ping_ , the private key and the target client`s hostname. In his test, basically the controller perform and ssh connection with the client node "ubuntu", the controller connects directly since is not necessary password authentication due to it is ssh-key based. Once, the controller has connected to the client node, it performs a query looking for a python interpreter.


```

[vagrant@rhel8 ~]$ ansible -m ping -u vagrant --private-key ubuntu.key ubuntu
192.168.56.13 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}


```

The controller will create a 'tux' user, append it to the sudoers file locally and remotely in their client nodes. Remember that the controller must use node ssh-key file for authenticate and proceed with the operation. Those .key are files that will be generated with scp utility in a vagrant environment

`user@host $ ansible --private-key ubuntu.key -u vagrant -m copy -a "src=tux dest=/etc/sudoers.d/"`

In the command above, the controller use the _tux_ file which contains the info which grants tux user passwordless privileges `("tux ALL=(root) NOPASSWD:ALL")`.


### 1.3.12. Help on Modules ###

List module with `ansible-doc -l` command.

`$ ansible-doc -l`

`$ ansible-doc -l | grep ping`

`$ ansible-doc user`

## 1.4. Creating Users ##

With user module ,is nedded to specify at least 01 user name as argument.
Must be run as root including the `-b` option (to become user = root)
You can delete the user with : `state=absent`

`$ ansible  192.168.56.2 -b -m user -a "name=fred"`

To delete a user:

`$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent"`

`$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent remove=true"`


## 1.5. Managing SSH Keys using Ansible ##
You must run the following code to add the public keys
of your remote hosts to your `known_hosts` file

`$ for h in 192.168.56.{2..4}; do ssh-keyscan $h >> ~/.ssh/known_hosts ; done`

Now is needed generate a SSH Key and distribute to our clients
in order we are not asked for entering password at everiy ssh connection.

`$ssh-keygen` (leave all by default)

After that, now is needed to verify if nodes in your 
inventory has active a python interpreter using the ping module

`$ ansible all -k -K -m ping`

- Remember that you dont have to have any file indicating the ip
and `ansible_connection=local`

After any hosts responds to ping module with success, you need
to distribute your ssh key to the `authorized_key` file.

`$ ansible all -k -K -m authorized_key -a " user='tux' state='present' key='{{ lookup('file','/home/tux/.ssh/id_rsa_ansible.pub')  }}'   "`

## 1.6. Create the user file for be added to sudoers.d folder in our managed hosts ##

`$ echo " tux ALL=(root) NOPASSWD: ALL  > tux"`

### 1.6.1. You can verify the syntax with : ###

`sudo visudo -cf tux`

### 1.6.2. Now, transfer this file to your managed nodes ### 

`$ ansible all -b -K -m copy -a " src='tux' dest='/etc/sudoers.d/tux'  "`

In this case, `all` means will be trasferred to all host in our inventory.

`-b` is used because will 'become' sudo, due to `-K` specified.

There is no needed anymore `-k` because we have already trasnferred our ssh public key to `authorized_keys` and prompt ssh password is not nedded.

`-m` is used to specify the `copy` module.

Finally `-a` is used for specify the other attributes enclosed by `""`.

If you try to run the previous command without -K ( sudo privilege ), will work too because we have already create the tux user file in sudoers.d directory


### 1.6.3. Creating User Account ###

First, will be created a user account in ad-hoc style


```

[vagrant@rhel8 ~]$ ansible --private-key ubuntu.key -u vagrant -m user -a "name=tux" ubuntu
192.168.56.13 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1002,
    "home": "/home/tux",
    "name": "tux",
    "shell": "/bin/sh",
    "state": "present",
    "system": false,
    "uid": 1002
}

```

- If you run again the command above, you will realize there is no new changes.
  

```

[vagrant@rhel8 ~]$ ansible --private-key ubuntu.key -u vagrant -m user -a "name=tux" ubuntu
192.168.56.13 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "append": false,
    "changed": false,
    "comment": "",
    "group": 1002,
    "home": "/home/tux",
    "move_home": false,
    "name": "tux",
    "shell": "/bin/sh",
    "state": "present",
    "uid": 1002
}


```

### 1.6.4. Listing Ansible Documentation Modules  ###

`$ ansible-doc -l`

`$ ansible-doc user` -> For viewing about user module documentation
I you want to view 'Examples', just type `\EXAMPLE`, and inside the response it will redirect the Example section. 

### 1.6.5. Playbooks ###

 - Single tab != single white-space
 - You can make vim as a valid yaml editor (~/.vimrc)
 
### 1.6.6. Comapring Tab to Spaces ###

- 8 spaces = 1 tab (With standard tab setting)
- `:set list` , helps to view that 
    - 8 spaces in vim
    - `^I` 1 tab in vim with standard tab setting

### 1.6.7. Sample of vimrc file ###

- For yaml file we set 
  * Auto indent
  * Expand Tabs to spaces
  * Tab Stop to 02 spaces
  * Shift Width to 02 spaces using auto-indent
  * Column Highlighting ad underlying.

- First line of the vimrc file
    `autocmd FileType yaml setlocal ai et ts=2 sw=2 cuc cul`

- Setting the vimrc file
    
    ```
      set bg=dark
      autocmd Filetype yaml setlocal ai et ts=2 sw=2 cuc cul
    
    ```
### 1.6.8. Sample how to format .nanorc file ###

- Open any editor you prefer and create in `$HOME/.nanorc` file.
- This file must content:

```
set autoindent
set tabsize 2
set tabstospaces

```

### 1.6.9. Sample of PLaybook ####

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

### 1.6.10. Using variables in Playbooks ###

```
---

- name: Play 1
  hosts: all
  tasks:
     - name: task 1
       debug:
         msg: "The hostname is {{ ansible_fqdn }}"

```

## 1.7. Playbook Summary ##

- Edit the vimrc file

   `autocmd FileType yaml setlocal ai et ts=2 sw=2 cuc cul`

- name of Playbook, and name of task are optional, but is extremely recommended for tshoot
- Every .yml file starts with 03 dash lines
- hosts field must be as follows (IP, group name)

      `hosts: 192.168.1.50`

      `hosts: group-centos`

- Remember disable gather_facts in your ansible script.

        `gather_facts: false`

### 1.7.1. Understanding why use/not use "gather facts" ###

Gather facts option is useful when you need to acquire information from the host. But maybe, sometimes is not necessary for a particular play, in that way is better not use in order to accomplish the task faster.

 - Here we have an example of playbook using facts.

```
---
- name: My first play
  hosts: all
  become: true
  tasks:
         - name: Install software
           package:
                   name: bash-completion
                   state: present
         - name: Show hostname
           debug:
                   msg: "This host is {{ ansible_hostname }}"

```

You can get all details of your machine by using the module "SETUP", you can do the following :

- `$ ansible <host/group> -m setup`

Where host, group or IP addressis valid field :) . Below is an example using the group _centos_ which contains 02 host with different IP address. I have also make a search using `grep` in order to filter network details about those hosts. 


```

[user@host ~]$ ansible centos -m setup | grep -i '192.168.56.'
192.168.56.3 | SUCCESS => {
            "192.168.56.3"
                "address": "192.168.56.3",
                "broadcast": "192.168.56.255",
                "network": "192.168.56.0"
192.168.56.2 | SUCCESS => {
            "192.168.56.2"
                "address": "192.168.56.2",
                "broadcast": "192.168.56.255",
                "network": "192.168.56.0"
```

Example: Using ad-hoc command and _setup_ module and attribute _filter_ for filtering results.


```

  [vagrant@rhel8 ~]$ ansible_connection=local ansible localhost -m setup \
  > -a "filter=ansible_os_family"
  localhost | SUCCESS => {
      "ansible_facts": {
          "ansible_os_family": "RedHat"
      },
      "changed": false
  }

```

## 1.8. Creating Users ##

- Look necessary documentation by doing `$ ansible-doc user`
  
### 1.8.1. Simplest User Creation ###

```
---

- name: User Creation
  hosts: all
  gather_facts: false
  become: true
  tasks:
    - name: Create User
      user:
        name: Jodi

```

### 1.8.2. Simplest User Deletion ###

```
---

- name: Delete User
  hosts: all
  become: true
  gather_facts: false
  tasks:
  - name: Delete User Account
    user:
      name: jodi
      state: absent
      remove: true

```

### 1.8.3. Create Multiple Users ###

```
---

- name: Multiple Items
  hosts: all
  become: true
  tasks:
    - name: create many users
      user:
        name: "{{ item }}"
      loop:
        - user1
        - user2
        - user3
```

user.yml  [file]

```
--- 

- name: Multiple Items
  hosts: all
  become: true
  tasks:
    - name: create many users
      user:
        name: "{{ user_name }}"

```
To create by using ad-hoc commands:

`$ ansible-playbook -e user_name=suki user.yml`
 
### 1.8.4. Create User (Example) [create_user_jodi.yml] ###

```
---
- name: Create user
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: create user
      user:
        name: 'jodi'
```

And is executed as follows:

`$ ansible-playbook create_user_jodi.yml `

If you prefer check syntax previously, you can type: 
`$ ansible-playbook create_user_jodi.yml --syntax-check `


To corroborate that the user `jodi` was added successfully, you can type:

`ansible all -m command -a 'getent passwd <user>'`

`ansible all -m command -a 'getent passwd jodi'`

The output:

```

192.168.56.2 | CHANGED | rc=0 >>
jodi:x:1002:1002::/home/jodi:/bin/bash
192.168.56.4 | CHANGED | rc=0 >>
jodi:x:1002:1002::/home/jodi:/bin/sh
192.168.56.3 | CHANGED | rc=0 >>
jodi:x:1002:1002::/home/jodi:/bin/bash

```

### 1.8.5. Delete User (Example) [delete_user_jodi.yml] ###

```
---
- name: Delete user
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: delete user
      user:
        name: 'jodi'
        state: 'absent'
        remove: true

```

### 1.8.6. Create Multiple User (Example) [create_multiple_user.yml] ###

```
---
- name: multiple user
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: create multiple user
      user:
        name: "{{ item }}"
      loop:
        - petu
        - barry
        - strinky
        
```

### 1.8.7. Delete Multiple User (Example) [delete_multiple_user.yml] ###

```
---
- name: multiple user
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: delete multiple user
      user:
        name: "{{ item }}"
        state: 'absent'
        remove: true
      loop:
        - petu
        - barry
        - strinky
        
```

### 1.8.8. Create User Using Variable Substitution (Example) [create_user_variable_substitution.yml] ###

```
---
- name: multiple user
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: create multiple user
      user:
        name: "{{ user_name }}"
        
```
- Consider that `user_name` is any variable that is not being used. 
- To proceed, just execute as follows

`$ ansible-playbook -e "user_name=jaiminho"  create_user_variable_substitution.yml `

## 1.9. User Passwords ##
Paswords must be encrypted, this can be done using ansible functions or using python script.

### 1.9.1. Example of script in Python3 ###

```
#!/usr/bin/python3
import sys, crypt

if len(sys.argv)==1 : sys.exit("You must specify a new password")
print(crypt.crypt(sys.argv[1], crypt.mksalt(crypt.METHOD_SHA512)))

```

The example above, will be used after. Now will be explained in case we use a native function of ansible for generating encrypted passwords.

```
---
- name: Create Users with Password
  hosts: all
  become: true 
  gather_facts: false
  tasks:
  - name: Create user account with encrypted password
    user:
      name: "{{ user_name}}"
      password: "{{ 'AnyPassword12345' | password_hash('sha512','anyvalforsalt') }}"
      update_password: on_create
    when: user_create == 'yes'
  - name: Delete user account 
    user:
      name: "{{ user_name }}"
      state: 'absent'
      remove: true
    when: user_create == 'no'

```

## 1.10. Create Ansible User ##

### 1.10.1. Create identical remote users for ansible ###

Until now, we have been created _standard user accounts_ using Ansible.
This account will need the following items:

- DevOps user account.
- Passwordless _sudo_ access.
- ssh key based	authentication from our	controller account.

### 1.10.2. Task to add _sudo_ access ###

At creating the user named as "devops" we can add paswordless access for the user.

```
- name: Setup sudo access
  copy:
        dest: /etc/sudoers.d/devops
        content: 'devops ALL=(ALL) NOPASSWD: ALL'
	validate: /usr/sbin/visudo -cf %s

```

From the code above, we have used the _copy_ module, and was specified the destination path of the new file called `devops` inside
the _sudoers.d_ folder, in that way it grants passwordless for any future command that it needs sudo access. The `devops` file must contains the indicated _content_. Finally, the content is verfied with the command `visudo -cf <file>` that is represented by %s.


### 1.10.3. Adding your local SSH Key ###

Until now we have bee using the _tux_ user account for modify and create things.
We will use that user for copy its SSH public key to the remote _devops_ account.

```
- name: Install Local User Key
  authorized_key:
        user: devops
	state: present
	manage_dir: true
	key: "{{ lookup{'file','/home/tux/.ssh/id_rsa.pub'}  }}"

```

### 1.10.4. Creating the devops account ###

Generate inside the `/users` folder  a _.vim_ file named _devops_.

`vim /home/tux/ansible/users/devops.yml`

```
---

- name: Deploy devops account
  hosts: all
  become: true
  tasks:
    - name: create account
      user:
	name: devops
    - name: sudo access
      copy:
	dest: /etc/sudoers.d/devops
        content: 'devops ALL=(ALL) NOPASSWD: ALL'
	validate: /usr/sbin/visudo -cf %s
    - name: ssh key
      authorized_key:
        user: devops
        state: present
	manage_dirs: true
	key: "{{ lookup( 'file', '/home/tux/.ssh/id_rsa.pub') }}"

```

### 1.10.5. Ad-hoc command to create user account in every inventory hosts ###

Will be createddd the `ansible` user in every host that belongs to the inventory file.

```
user_password=$( openssl passwd -6 Password1 )
[user@host]$ echo $user_password
$6$aqBxnzLdlawurBaM$IXSz4f5tc3QF08C6i98IVHpZpcl5fvQkSYOCZVaqDbKkXGqS2QlmTH502vnZKHJvWXNEiMPozLv2JTWD1AoKf1
[user@host]$ ansible all -kKbm user -a "name=ansible password=$user_password"
SSH password:
BECOME password[defaults to SSH password]:
```
This is the output:

```
192.168.56.4 | CHANGED => {
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1005,
    "home": "/home/ansible",
    "name": "ansible",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "/bin/sh",
    "state": "present",
    "system": false,
    "uid": 1005
}
192.168.56.2 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1005,
    "home": "/home/ansible",
    "name": "ansible",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1005
}
192.168.56.3 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1005,
    "home": "/home/ansible",
    "name": "ansible",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1005
}

```

For verifying the account creation, you can perform this:

```
[user@host]$ getent passwd ansible
ansible:x:1005:1005::/home/ansible:/bin/bash
[user@host]$ sudo getent shadow ansible
ansible:$6$aqBxnzLdlawurBaM$IXSz4f5tc3QF08C6i98IVHpZpcl5fvQkSYOCZVaqDbKkXGqS2QlmTH502vnZKHJvWXNEiMPozLv2JTWD1AoKf1:18854:0:99999:7:::

```
### 1.10.6. Allowing Passwordless Sudo Access for `ansible` user ###
- Create one file that contains the following fields

`echo "ansible ALL=(root) NOPASSWD: ALL" > ansible`

- Corroborate if syntax is ok: `sudo visudo -cf ansible`

- Copy to /etc/sudoers.d at your destination machines

 `$ ansible all -bkK -m copy -a "src=ansible dest=/etc/sudoers.d/ansible" `

### 1.10.7. SSH Key authentication ###

- Here, will be trasnferred our public key that is located in `home/<other_user>/.ssh` to  ansible user folder at our destination controlled clients

` $ ansible all -bkKm authorized_key -a "user='ansible' state='present' key='{{ lookup( 'file', '/home/tux/.ssh/id_rsa.pub' ) }}' " `




## 1.11. Install Multiple Package with Playbook  ##
A briefly playbook [install-multi-pkgs.yml] for you understand how to install package in your inventory hosts.

```
---
- name: My second play
  hosts: all
  become: true
  tasks:
          - name: Install many softwares
            package:
              name:
                    - bash-completion
                    - vim
                    - tree
                    - nano
              state: present
          - name: Show hostname where it has been installed
            debug:
                    msg: "This host is {{ansible_hostname}}"

```

Now, you have to execute it as follows:

- `$ ansible-playbook install-multi-pkgs.yml `

The output:

```
[user@host]$ ansible-playbook install-multi-pkgs.yml

PLAY [My second play] **********************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************
ok: [192.168.56.2]
ok: [192.168.56.3]
ok: [192.168.56.4]

TASK [Install many softwares] **************************************************************************************************************************************
ok: [192.168.56.2]
changed: [192.168.56.3]
changed: [192.168.56.4]

TASK [Show hostname where it has been installed] *******************************************************************************************************************
ok: [192.168.56.2] => {
    "msg": "This host is bob"
}
ok: [192.168.56.3] => {
    "msg": "This host is alice"
}
ok: [192.168.56.4] => {
    "msg": "This host is ubuntu"
}

PLAY RECAP *********************************************************************************************************************************************************
192.168.56.2               : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.56.3               : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.56.4               : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
## 1.12. Working with Variables and Facts ##

For example CentOS and Ubuntu use different package management, `yum` for CentOS and `apt` for Ubuntu.
The process of intallation of different packages can be optimized by using conditional and variables to detect which distribution is being used.

For example _Apache Web Server_ is treated with the follwing names:

- Ubuntu (apache2)
- CentOS (httpd)

The default admin groups are:

- Ubuntu (sudo)
- CentOS (wheel)

The use of variables can be performed in host groups to represent group names as an example.

### 1.12.1. Using Multiple Plays ###

If we use _host groups_ to deploy a play, for example 02 groups called
_Ubuntu_ and _CentOS_ we can use 02 plays.

```
---
- name: Ubuntu Play
  hosts: ubuntu
  tasks:
   - name: install apache
     apt:
      name: apache2

``` 

### 1.12.2. Using Facts ###

It is useful when an specific task must be targeted to an specific distribution. The clause `when` should be used, as similar as
a conditional statement. In that way, you can use just only one play with multiple tasks.

```
---
- name: Deploy apache
  hosts: all
  tasks:
   - name: install apache
     yum:
      name: httpd
     when: ansible_distribution == 'CentOS'

```
Another example:

```
---
- name: Deploy Apache
  hosts: local
  become: true
  gather_facts: true
  tasks:
   - name: install apache centos
     yum:
      name: httpd
     when: ansible_distribution == 'CentOS'
   - name: install apache ubuntu
     apt:
      name: apache2
     when: ansible_distribution == 'Ubuntu'

```

### 1.12.3. Consider Inventory Variables ###

It is recommended create those variables in our folder `group_vars` previously created.

```
$ mkdir groups_vars/
$ echo "admin: wheel" > group_vars/centos
$ echo "web_package: httpd" >> group_vars/centos
$ echo "admin : sudo" > group_vars/ubuntu
$ echo "web_package: apache2" >> group_vars/ubuntu

```

### 1.12.4. Playbook using variables "Admin Groups" ###

Using variables can be a good idea to caster for differences

```
---
- name: Create Admin User
  hosts: webservers
  gather_facts: no
  become: true
  tasks:
    - name: Create User
      user:
        name: bob
        groups:
         - "{{ admin }}"

```

### 1.12.5. Playbook Using Variables "Package MOdule" ###

The package module is nice because it allows the correct _apt_ or  _yum_ package management
be detected. WIth the correct variable set in `group_vars/` this works good.

```
---
- name: Install apache
  hosts: webservers
  gather_facts: no
  become: true
  tasks:
  
   - name: install apache
     package:
       name: "{{ web_package }}"
       state: latest
```

## 1.13. Lab Time! ##

Will be create a new directory `lamp` inside `/home/tux/ansible/users/` path. And will be copied the follwing files from the parent folder.

- ansible.cfg
- inventory

```
$ cd /home/tux/ansible/users
$ mkdir -p lamp/{host,group}_vars
$ cp ../users/ansible.cfg .
$ cp ../users/inventory .

```

Inside the new folder `lamp`, will be created files:

```
echo "ansible_connection: local" > host_vars/192.168.56.2
echo "admin: wheel" >> group_vars/centos
echo "web_package: httpd" >> group_vars/centos
echo "admin: sudo" >> group_vars/ubuntu
echo "web_package: apache2" >> group_vars/ubuntu

```

We create a simple .yml file (user.yml):

```
---
- name: play
  hosts: all
  tasks:
    - name: tasks
      user:
        name: devops
        groups: "{{ admin  }}"

```

Executing the file `$ ansible-playbook user.yml` will assign the `devops` account to the group `sudo`, using the alias
or variable created in _*group_vars/ubuntu*_ .
 
### 1.13.1. Installing Apache (Multiple Plays) ###

Create the file `apache-multi-play.yml`:

```
---
- name: ubuntu
  hosts: ubuntu
  tasks:
    - name: install apache
      apt:
        name: apache2
        state: latest
- name: centos
  hosts: centos
  tasks:
    - name: install apache
      yum:
       name: httpd
       state: latest
   
```
To execute, `$ ansible-playbook apache-multi-play.yml` .
Obs: This method is difficult to maintain in a long term because of code duplication, but is simple to implement.
Obs: May occur that at running the playbook may gives an error due to the repository is not updated, I recommend
change the server of update to the 'main server'. You can make it using the GUI or by terminal just by editing the
`/etc/apt/sources.list` file. You should take off any country code that precedes the [xy].archive.ubuntu.com.
```
sed -r -i "s/[a-zA-Z]{1,3}\.archive/archive/g" /etc/apt/sources.list

```
### 1.13.2. Installing Apache ( Logic ) ###

Create the file `apache-using-logic.yml`:

```
---
- name: apache
  hosts: all
  tasks:
    - name: install apache ubuntu
      apt:
        name: apache2
        state: latest
      when: ansible_distribution == 'Ubuntu'

    - name: install apache centos
      yum:
        name: httpd
        state: latest
      when: ansible_distribution == 'CentOS'
   
```

To execute, `$ ansible-playbook apache-using-logic.yml` .

### 1.13.3. Installing Apache ( Variables) ###

Create the file `apache-using-variables.yml`:

```
---
- name: apache
  hosts: all
  tasks:
    - name: install apache ubuntu
      package:
        name: "{{ web_package }}"
        state: latest
   
```

To execute, `$ ansible-playbook apache-using-variables.yml` .
dc





