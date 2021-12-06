### Ansible-Installation ###
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

### Configuration Hierarchy ###
Environmental Variable: `ANSIBLE_CONFIG`

ansible.cfg  in Working Directory

`$HOME/.ansible.cfg`

`/etc/ansible/ansible.cfg`

`$ ansible --version` -> Show config file

`echo > ~/.ansible.cfg`

### Show current file contents ###

`$ ansible-config view`

### Show all configuration ###
`$ ansible-config list`

### Show current settings ###
`$ ansible-config dump`

### Show only non-default settings ###
It shows what was has changed from reference main config file

`$ ansible-config dump --only-changed`

```
[vagrant@rhel8 ~]$ ansible-config dump --only-changed
DEFAULT_BECOME(/home/vagrant/.ansible.cfg) = True
DEFAULT_HOST_LIST(/home/vagrant/.ansible.cfg) = ['/home/vagrant/inventory']
DEFAULT_REMOTE_USER(/home/vagrant/.ansible.cfg) = tux

```
## Sample of configuratio file ##
```
[defaults]
inventory=inventory ; set inventory file in the same working directory

remote_user = tux

[privilege_escalation]
become = true; or set in play when needed
become_method = sudo

```

## Ansible Inventory ##
This is a list of hosts,groups and variables that normally or
by default is in `/etc/ansible/hosts`.

### Example of an inventory file ###
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


### Query Inventory ###
This is the way how you make request to query
for listing hosts in your inventory file

* If you ommit `-i` , you will look up in the inventory
file configured

`$ ansible -i hosts --lists-hosts ubuntu`

`$ ansible -i hosts --list-hosts webservers`

### Separate Hosts and Variables ###
Is a better practice to separate hosts and groups in differnet
folders for example "`host_vars`, `group_vars`" groups.

`$ mkdir ./host_vars`
`$ echo "ansible_connection: local" > host_vars/192.168.56.2`

### Ad-hoc commands ###

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

`-b` -> to elevate privileges

### Basic Configuration ###
From inventory hosts we will perform a simple script for
scan the publick ssh key cached  and add it to known_hosts file and
be accepted when we try to establish a secure communication

`$ for h in 192.168.56.{2..4}; do ssh-keyscan $h >> ~/.ssh/known_hosts ; done`

`$ ssh-keygen` (for generation)

### Ping Hosts ###
This is not related to ICMP protocol, it is called like that but really
this is a module that look for a python interpreter active in the remote hosts
(`-k` , to prompt ssh password; `-K` to prompt for SUDO password)

`$ ansible all -k -K -m ping` 

###  Distribute SSH Key ###
Distribution of the ssh key in all nodes where is created the same user tux
, add the ssh key in authorized_keys file
 
```$ ansible all -k -K -m authorized_key \
-a " user='tux' state='present' \ 
key='{{ lookup('file','/home/tux/.ssh/id_rsa.pub') }}'  "
```

### Copy Sudoers Files ###
To allow passwordless for not being asked everytime for sudo rights

`$ echo " tux ALL=(root) NOPASSWD:ALL" > tux`
 
To verify if syntax is correct, do:

`$ sudo visudo -cf tux`

Copy process for all inventory hosts using `-b` to become sudo and elevate
prvileges using `-K`, using copy module `-m` and specify the `-a` argument "..."...

`$ ansible all -b -K -m copy -a "src=tux dest=/etc/sudoers.d/tux"`

### Help on Modules ###
List module with `ansible-doc -l` command.

`$ ansible-doc -l`

`$ ansible-doc -l | grep ping`

`$ ansible-doc user`

## Creating Users ##
With user module ,is nedded to specify at least 01 user name as argument.
Must be run as root including the `-b` option (to become user = root)
You can delete the user with : `state=absent`

`$ ansible  192.168.56.2 -b -m user -a "name=fred"`

To delete a user:
`$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent"`

`$ ansible 192.168.56.2 -b -m user -a "name=fred state=absent remove=true"`


## Managing SSH Keys using Ansible ##
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

## Create the user file for be added to sudoers.d folder in our managed hosts ##
`$ echo " tux ALL=(root) NOPASSWD: ALL  > tux"`

### You can verify the syntax with : ###
`sudo visudo -cf tux`

### Now, transfer this file to your managed nodes ### 
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
 
### Comapring Tab to Spaces ###
- 8 spaces = 1 tab (With standard tab setting)
- `:set list` , helps to view that 
    - 8 spaces in vim
    - `^I` 1 tab in vim with standard tab setting

### Sample of vimrc file ###
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
### Sample how to format .nanorc file ###
- Open any editor you prefer and create in `$HOME/.nanorc` file.
- This file must content:

```
set autoindent
set tabsize 2
set tabstospaces

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

```
---

- name: Play 1
  hosts: all
  tasks:
     - name: task 1
       debug:
         msg: "The hostname is {{ ansible_fqdn }}"

```


## Playbook Summary ##

- Edit the vimrc file
   `autocmd FileType yaml setlocal ai et ts=2 sw=2 cuc cul`
- name of Playbook, and name of task are optional, but is extremely recommended for tshoot
- Every .yml file starts with 03 dash lines
- hosts field must be as follows (IP, group name)
      `hosts: 192.168.1.50`
      `hosts: group-centos`
- Remember disable gather_facts in your ansible script.
        `gather_facts: false`

### Understanding why use/not use "gather facts" ###

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

## Creating Users ##
- Look necessary documentation by doing `$ ansible-doc user`
### Simplest User Creation ###
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

### Simplest User Deletion ###

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

### Create Multiple Users ###

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
 
### Create User (Example) [create_user_jodi.yml] ###
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
### Delete User (Example) [delete_user_jodi.yml] ###

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

### Create Multiple User (Example) [create_multiple_user.yml] ###

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

### Delete Multiple User (Example) [delete_multiple_user.yml] ###

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

### Create User Using Variable Substitution (Example) [create_user_variable_substitution.yml] ###

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

%% User Passwords %%
Paswords must be encrypted, this can be done using ansible functions or using python script.

### Example of script in Python3 ###
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

## Create Ansible User ##

### Create identical remote users for ansible ###

Until now, we have been created _standard user accounts_ using Ansible.
This account will need the following items:

- DevOps user account.
- Passwordless _sudo_ access.
- ssh key based	authentication from our	controller account.

### Task to add _sudo_ access ###

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


### Adding your local SSH Key ###

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

### Creating the devops account ###

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

### Ad-hoc command to create user account in every inventory hosts ###

I will create the `ansible` user in every host that belongs to the inventory file.
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
### Allowing Passwordless Sudo Access for `ansible` user ###
- Create one file that contains the following fields

`echo "ansible ALL=(root) NOPASSWD: ALL" > ansible`

- Corroborate if syntax is ok: `sudo visudo -cf ansible`

- Copy to /etc/sudoers.d at your destination machines

 `$ ansible all -bkK -m copy -a "src=ansible dest=/etc/sudoers.d/ansible" `

### SSH Key authentication ###

- Here, will be trasnferred our public key that is located in `home/<other_user>/.ssh` to  ansible user folder at our destination controlled clients

` $ ansible all -bkKm authorized_key -a "user='ansible' state='present' key='{{ lookup( 'file', '/home/tux/.ssh/id_rsa.pub' ) }}' " `




## Install Multiple Package with Playbook  ##
A biefly playbook [install-multi-pkgs.yml] for you understand how to install package in your inventory hosts.

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

## Working with Variables and Facts ##

For example CentOS and Ubuntu use different package management, `yum` for CentOS and `apt` for Ubuntu.
The process of intallation of different packages can be optimized by using conditional and variables to detect which distribution is being used.

For example _Apache Web Server_ is treated with the follwing names:

- Ubuntu (apache2)
- CentOS (httpd)

The default admin groups are:

- Ubuntu (sudo)
- CentOS (wheel)

The use of variables can be performed in host groups to represent group names as an example.

### Using Multiple Plays ###

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

### Using Facts ###

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

### Consider Inventory Variables ###

It is recommended create those variables in our folder `group_vars` previously created.

```
$ mkdir groups_vars/
$ echo "admin: wheel" > group_vars/centos
$ echo "web_package: httpd" >> group_vars/centos
$ echo "admin : sudo" > group_vars/ubuntu
$ echo "web_package: apache2" >> group_vars/ubuntu

```

### Playbook using variables "Admin Groups" ###

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

### Playbook Using Variables "Package MOdule" ###

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

## Lab Time! ##

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
 
### Installing Apache (Multiple Plays) ###

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
### Installing Apache ( Logic ) ###

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



### Installing Apache ( Variables) ###

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





