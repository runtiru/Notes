# 04/10/23

## User Creation

* ssh (scure Shell):-
  * is a network protocol used for secure remote access to computer systems over a potentially unsecured network.

* Linux:-
  * linux is a kernel

* Kernel:-
  * core oprating system which capability speake whith hardware giveing simple interphase

* Distubuations
* Shell

* Debian Family  
    - Ubuntu
    - Kali
    - Debian

* Redhat Family
    - Redhat
    - Fedora
    - Centos
    - RHEL
    - Amazon Linux

## 05/10/23

[https://directdevops.blog/2023/10/05/devops-classroomnotes-05-oct-2023/]

## Create a user and Setting up password less authentication between linux machines:-

* Create 2 instances
    server-1 and server-2 & login that matchane
```sh
ssh -i ~/downloads`tab`\<key.pem> ubuntu@<IP>   ---> Both
```

* passwd authuntication yes
```sh
sudo vi(nano) /etc/ssh/sshd_config  ---> Both users
```
  PasswordAuthentication `yes`
   `Esc:wq!`

* restaer the server
```sh
sudo systermctl restart sshd  ---> Both users
```

* create user
```sh
sudo adduser devops ----> Both users
```
Password: runner

* communicate with 2 servers
```sh
ssh devops@<private ip of server2>  ---(1)
```
Password: **** & exit

* Adding user to sudo     ---->Both users (RT (14:00))
```sh
sudo visudo
```
In %sudo-->
  devops ALL=(ALL:ALL) NOPASSWD:ALL
<Ctrl+o enter ctrl+x -->

* switch user   ---> oth users
```sh
su devops
  passwd ****
```

* home directory    ---> Both users
```sh
cd ~
pwd
/home/devops

sudo apt update   ---> Both users
```

* login form one server to another server   ----->RT (21:00)
```sh
ssh <private ip server2>  ---(1)  
Password: *****

& eixt
```

## setting password less authountication in Both servers

* create key pair in server1    ---(1)
```sh
ssh-keygen
```

* check the both keys
```sh
ls ~/.ssh/
```

  id_rsa   id_rsa.pub   known_hosta
    - ~/.ssh/id_rsa   ==> private key
    - ~/.ssh/id_rsa.pub ==> public key

`private key`
  ^ ls ~/.ssh/id_rsa
 /home/devops/.ssh/id_rsa
    ^ cat /home/devops/.ssh/id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----

`public key`
  ^ ls ~/.ssh/id_rsa.pub
 /home/devops/.ssh/id_rsa.pub
    ^ cat /home/devops/.ssh/id_rsa.pub

* copy the public key into sercer2      ---(1)
```sh
ssh-copy-id devops@<private ip2>
password:******
```

In server2
```sh
ls ~/.ssh/
```
authorized_keys = (private of server1)
```sh
cat ~/.ssh/authorized_keys
```

* After the ssh-copy-id is success, then we can login directly by using ip address as both machines have same username and password less authentication is setup.
* switch to one server to another server.

* In server1
```sh
ssh <ip adderss of server2>
server1 changed to servewr2
exit >
```
==================================
# Ansible setup :-

* we have two machines with common user name devops,
* sudo permissions and password less authentication setup between server 1 and server 2,
* From now server 1 will be called as `Ansible Control node` and server 2 as `node 1`

* Ensure python:3 is installed
```sh
python3 --version   ------2
   Python 3.10.6
```
<:- If python is not installed `install pythone on ubuntu` -->

`Installing and upgrading Ansible with pip`
[https://docs.ansible.com/ansible/latest/installation_guide/index.html]

## Install ansible      -----RT (35:00)

[https://docs.ansible.com/ansible/latest/installation_guide/index.html]

* We have two approaches to install ansible
  - Debian --> apt
  - nRedHet --> yam (dnf)

`Debian` :-
* apply those commands on server1 -----(1)

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```

    ^ ansible --version - ansible [core 2.15.4]

## Test ansible connectivity from ansible `control node` to `node1`

* Create a file with node 1 ip address in it
  * Create a file
```sh
echo <Ip address-2> > hosts
cat hosts
  172.31.17.52
```

* execute the following command `ansible -m ping -i hosts all`
    ^ ansible -m ping -i hosts all

<---SUCCESS--->

-----------------------------------------------------

* Changing the host     ---->RT (46:00)
```sh
vi hosts    ----(1)
  172.31.17.52
  (localhost)

ansible -m ping -i hosts all
```

* Its dosent move `-X-`
```sh
ssh-copy-id localhost
   Password:*****

ansible -m ping -i hosts all
```
<---SUCCESS--->

```sh
ansible --help | less (more)
```

* connect to ansible ----(1)
```sh
ansible -i hosts -u devops -K -m ping all
   Password: ******
```
<---SUCCESS--->

* Ansible can communicte other machine useing two ways:-
  * key based authountication
  * password based authountication

=============

## 06/10/23

# YAML

[https://directdevops.blog/2023/10/06/devops-classroomnotes-06-oct-2023/]

* This is data representation language which uses name values
    `NAME: VALUE`

* YAML is inspired from python, so indentation’s become mandatory
* YAML files generally have `.yaml` or `.yml` as extensions

Lets categorize data
    - Scalar/Simple
      - text
      - number
      - boolean
    - Complex
      - list/array

```bash
---
name: test
mobile: '999999999'
email: test@test.com
CareerObjective: |
  A motivated individual with in-depth knowledge of languages 
  and development tools, seeking a position in a growth-oriented 
  company where I can use my skills to the advantage of the 
  company while having the scope to develop my own skills.
ProfessionalSummary:
  - Involved in designing CI/CD pipleines
  - Hands on experience in Develpoing Ansible playbooks
Skills:
  os:
    - windows
    - linux
  cm:
    - Ansible
  container:
    - Docker
Work experience:
  - company: xyz limited
    duration: Dec 2021 - present
    designation: DevOps Engineer
    RandR:
      - Ensuring Pipelines are healthy
      - Developing playbooks
  - company: abc limited
    duration: Dec 2019 - Dec 2021
    designation: DevOps Engineer
    RandR:
      - Ensuring Pipelines are healthy
      - Developing playbooks
```

## Basic structure of Ansible playbook

```bash
---
- name: <name of playbook - text>
  hosts: <where to execute-text>
  become: <need sudo permissions -bool>
  tasks: # <list of task>
  - name: Ensure apache is at the latest version # name of task
    ansible.builtin.yum: # module name
      name: httpd # module arguments
      state: latest # state
```

===========

## 07/10/23

## Ways of Working in Ansible

    - Figure out the manual steps
    - Execute and verify if they are working
    - for each manual step findout an ansible module which can help.

## Ansible Module..!

* this is the smallest unit of work in Ansible
* Module takes some inputs which are generally referred as parameters and it has state.

## Ansible Execution Approaches:-

* Adhoc command:
  * This uses the following structure and it is used for `non repetitive tasks`

```bash
ansible -m "<module-name>" -a "<arguments>" <where>
```

* Playbook:
  * This is yaml representation of sequence of commands and it is designed to be reptitive.

## Activity: install apache server on node 1

* it any application deploy to do manual steps  if the application can work or not...

* manual steps
```bash
sudo apt update
sudo apt install apache2 -y
```

# Activity1:
  * Write a yaml file & create 2 files 
      `activity1.yaml`
      `hosts`

1. activity1.yaml
```bash
---
- name: run apache
  become: yes
  hosts: all
  tasks:
    - name: Install apache2 on ubuntu
      ansible.builtin.apt:
        name:
          - apache2
        state: prestnt
        update_cache: yes         
```

hosts

```sh
private ip address of node2
```

* Syntax check
```bash
ansible-playbook --syntax-check -i <path to inventory> <path to playbook.yaml>
ansible-playbook --syntax-check -i hosts activity1.yaml
```

* Check the execution (dry run). Note this is not always correct
```bash
ansible-playbook --check -i <path to inventory> <path to playbook.yaml>
ansible-playbook --check -i hosts activity1.yaml
```

* Now lets execute the playbook
```bash
ansible-playbook -i <path to inventory> <path to playbook.yaml>
ansible-playbook -i hosts activity1.yaml
```

* Uninstall Apache2 in AnsibleNode in manual
  - login into node1 (ansiblemaster node)
    ^ ssh <private IP node1>

* delete manual
```sh
sudo apt purge apache2 -y
```

* once uninstall apache in master node, 
  ansible automatically create again the application.....
```sh
ansible-playbook -i hosts activity.yaml\
```

## Actual state

* The actual state refers to the current state or configuration of a system or set of systems.
* It is the state of the system as it exists at the moment when you run Ansible.

## Desired state

* The desired state is the state or configuration that you want your system or systems to be in.
* It represents the end state you are aiming to achieve after running an Ansible playbook.

## Configuration Drift

* the situation where the configuration of a managed system changes over time, deviating from the desired or defined state.
* whre the ansible present actual state or desired state.....

# Activity 2

     Install php on apache server    ----> RT (47:00)

## PHP
* Popular Programing language
* devoping language for web applications..
  * Eg: FB devloped in PHP language
  
* Manual steps:
```bash
cd /tmp
sudo apt udpate 
sudo apt install apache2 -y

sudo apt install php libapache2-mod-php php-mysql -y
```

* Lets create a file `/var/www/html/info.php` with the following content.

```
<?php phpinfo(); ?>
```

    - in the test VM 
        ^ cd /tmp
        ^ sudo -i
        ^ echo '<?php phpinfo(); ?>'
        ^ echo '<?php phpinfo(); ?>' > /var/www/html/info.php
        ^ cat /var/www/html/info.php

    - now access the ip address  --> apache server
          ip//var/www/html/info.php   ---> php server
----------------------

* Play Book:-
  * create folder `Php`  inside php 2 files..
        - `activity2`
        - `hosts.ini`
        - `info.php`

* activity2.yml
```bash
---
- name: Install PHP
  become: yes
  hosts: php
  tasks:
    - name: install apache
      ansible.builtin.apt:
        name:
          - apache2
        state: present
        update_cache: yes
    - name: install php packages
      ansible.builtin.apt:
        name:
          - php
          - libapache2-mod-php
          - php-mysql
        state: present
        update_cache: yes
    - name: copy php file
      ansible.builtin.copy:
        src: info.php
        dest: /var/www/html/info.php
```

hosts.ini
```sh
[php]
172.31.43.40
```

info.php
```sh
<?php phpinfo(); ?>
```

```sh
ansible-playbook --syntax-check -i hosts.ini activity2.yml
ansible-playbook --check -i hosts.ini activity2.yml
ansible-playbook -i hosts.ini activity2.yml
```

## Activity 3: Install PHP on redhat  ---> RT (01:24:00)

* Perform the activity2 on redhat

* manual steps:
```sh
sudo dnf install httpd -y
sudo dnf install php php-cli php-common php-gd php-mysqlnd php-pdo -y
```

Lets create a file `/var/www/html/info.php` with the following content

```sh
<?php phpinfo(); ?>

cd /tmp
sudo -i
echo '<?php phpinfo(); ?>'
echo '<?php phpinfo(); ?>' > /var/www/html/info.php
cat /var/www/html/info.php
```
    - now access the ip address  --> apache server
          ip//var/www/html/info.php   ---> php server

* I need to setup a redhat vm with devops user.
  * install RedHat VM (free)
      - login the VM...
  - [connect to ssh clint]
```sh
ssh ec2-user@<public ip>
```

  * create a user `runner`
```sh
sudo adduser runner
sudo passwd runner
```
  - New password: ****
  - Retype new password: ****

  * Password based authountication..
```sh
sudo vi /etc/ssh/sshd_config
  PasswordAuthentication `yes`
  
sudo systemctl restart sshd
```

  * Add sudo to  user
  - sudo usermod -aG wheel runner this is password based, we need password less
```sh
sudo visudo 
    wheel     ALL-(ALL)     NOPASSWD: ALL
    runner    ALL-(ALL)     NOPASSWD: ALL

exit
```
* now user name chege like-->
```sh
ssh runner@<ip address>
  password: ******

sudo yun update
  <--no-->

sudo dnf --help
```

* now comming to the ansible-controle plane
```sh
ssh-copy-id runner@<ip>
  password: *****
```

* cross check whether its is work or not...
```sh
ssh <public ip of redhat>
ssh-copy-id <public ip>
```
----------------

* Create a file `readhat`
    - activity3.yml
    - hosts.ini

* activity3.yml
```bash
---
- name: activity 3 install apache and php
  become: yes
  hosts: all
  tasks:
    - name: install apache
      ansible.builtin.dnf:
        name:
          - httpd
          - php
          - php-cli 
          - php-common
        state: present
    - name: create info.php
      ansible.builtin.copy:
        content: '<?php phpinfo(); ?>'
        dest: /var/www/html/info.php
```

hosts.ini - `private ip adress of redhat`
```sh
ansible-playbook --syntax-check -i hosts.ini activity3.yaml
ansible-playbook --check -i hosts.ini activity3.yaml
ansible-playbook -i hosts.ini activity3.yaml
```

  -> once done copy public ip of node2 (readhat) web:--> `httpd://<ip>/info.php`

  -> application was not run beauser redhat needs `service module`

* activity3.yaml
```sh
continue:-
    - name: ensure httpd is running
      ansible.builtin.service:
        name: httpd
        enabled: yes
        state: started
```
```sh
ansible-playbook --syntax-check -i hosts.ini activity3.yaml
ansible-playbook --check -i hosts.ini activity3.yaml
ansible-playbook -i hosts.ini activity3.yaml
```
   -> once done copy public ip of node2 (readhat) web:--> `httpd://<ip>/info.php`

## Activity:- 
  - Use the same playbook for ubuntu and redhat machines

* To do this activity, the two topics which we need to understand are
      - inventory groups
      - facts

============

## 08/10/23

## Inventories in Ansible

* Inventory is collection of nodes.

* Inventory is of two types
      1. Static
      2. Dynamic

* Inventory can be written in two formats
    1. ini format
    2. yaml format

* ini format
```sh
ipaddress/name

[group1]
ipaddress/name
ipaddress/name

[group2]
ipaddress/name
ipaddress/name
```

* Create folder `Inventory`
      - example1
          add 3 nodes of public ip
      - example2

exaple1

```bash
52.90.169.156
18.209.176.46
34.229.22.99
```
```sh
ansible -i example1 all --list-host
```

example2

```sh
[local]
52.90.169.156

[nodes]
18.209.176.46
34.229.22.99

[ubuntu]
52.90.169.156
18.209.176.46

[redhat]
34.229.22.99
```
```sh
ansible -i example2 local --list-hosts
ansible -i example2 nodes --list-hosts
```

## fact collection
  - fact is some information about ansible machen

* Create a inside `Inventory` folder `facts.json`

* How to collect facts
  * once done inventory file, to setup .....

```sh
ansible -i example2 local -m setup
```

  - if you want to need less or only json formet...
```sh
ansible -i example2 local -m setup > /tmp/facts.json
cat /tmp/facts.json
```

  - now the copy the all facts.... paste the `facts.json`

facts.json - 
NOTE: im not add all the facts due to space issue....

```sh
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "172.31.47.184"
        ],
        "ansible_all_ipv6_addresses": [
            "fe80::c29:b2ff:fec9:d9e7"
        ],
        "ansible_apparmor": 
     
    n/bash",
        "ansible_user_uid": 1001,
        "ansible_userspace_architecture": "x86_64",
        "ansible_userspace_bits": "64",
        "ansible_virtualization_role": "guest",
        "ansible_virtualization_tech_guest": [
            "xen"
        ],
        "ansible_virtualization_tech_host": [],
        "ansible_virtualization_type": "xen",
        "discovered_interpreter_python": "/usr/bin/python3",
        "gather_subset": [
            "all"
        ],
        "module_setup": true
    },
    "changed": false
}
```

* change a module:-
```sh
ansible -i example2 local -m setup -a "filter=*os*"
ansible -i example2 local -m setup -a "filter=**os**"

ansible -i example2 all -m setup -a "filter=**os**"
```

## Activity 4: installing php in both redhat and ubuntu

* What is needed?
  * inventory
  * facts
  * using facts with conditionals.

===================

## 10/10/23

### Install TOMCAT ..by RamJagadesh sir

create a instance ubuntu (t2.medium)

* Manual stepts:
  * tomcat install on ubuntu22.04
    - install java11

  * install tomcat setup
```sh
sudo useradd -m -d /opt/tomcat -U -s /bin/false tomcat
sudo apt update
sudo apt install default-jdk
java -version
cd /tmp
```

  * web:- tomcat packages tar file
    - chose the latest version `10.1.15`
    * core:
      - tar.gz (pgp, sha512) - copy this zip file (rightclick)
```sh
wget <https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.15/bin/apache-tomcat-10.1.15.tar.gz>

ls
  apache-tomcat-10.1.15.tar.gz

sudo tar xzvf apache-tomcat-10*tar.gz -C /opt/tomcat --strip-components=1
cd ..
cd /opt
ls -l
```
  * give file permisions for /tomcat file
```sh
sudo chmod 755 tomcat
ls -l
```
  done the r,w permitions..
```sh
cd /tomcat (/opt/tomcat$)
cd ..
cd ..
cd ..   (~$)
```

tomcat ownership
```sh
sudo chown -R tomcat:tomcat /opt/tomcat/
sudo chmod -R u+x /opt/tomcat/bin
```

* create a service
  - service file
    - serves file give a reloade for your application
      - once your vm was stoped the serve file cat resart automatically your application...

  * we need to java (we have already install java11)
```sh
java --version (or) ^ sudo update-java-alternatives -l
```

  we needs to bin file, give r,w permitions on /bin file
```sh
sudo chmod 755 /opt/tomcat/bin
cd /opt/tomcat/bin
ls
```
  some jar, xml, sh files....
```sh
sudo sh startup.sh
```
  now the tomcat service run....
    - take the public ip of vm <ip:8080>
```sh
sudo ./shutdown.sh
```
    - take the public ip of vm <ip:8080>

  now the application was unable to access....
    becose there no serves file....

  * create a service
      - first move to home direcoty
```sh
cd ~
sudo vi (nano) /etc/systemd/system/tomcat.service
```
  add to service file
```bash
[Unit]
Description=Tomcat
After=network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
Environment="CATALINA_BASE=/opt/tomcat"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
```
```sh
sudo systemctl daemon-reload
```
  - once again give a file permision foe the your application not get the commad...
```sh
sudo chown -R tomcat:tomcat /opt/tomcat/
      sudo chmod -R u+x /opt/tomcat/bin -->

sudo systemctl start tomcat.service
sudo systemctl status tomcat.service
```

  now check service run are not....??
```sh
sudo systemctl enable tomcat.service
```

  its careate a symlink (symbalic link) - its reeboot your application
    and restart your application

  - take the public ip of vm <ip:8080>

## playbook for tomcat

* create tomcat user and directory
```sh
sudo useradd -m -d /opt/tomcat -U -s /bin/false tomcat
```

* update & install packages
  * default-jdk

* go to temp dir & download tomcat packages
  * /tmp/apache-tomcat-10.1.15.tar.gz

* unzip tomcat files to (unarchive module in ansible)
  * /tmp/apache-tomcat-10.1.15.tar.gz
  * /opt/tomcat
  * --strip-components=1

* unzip tomcat files to (file module)    -----> RT (01:15:00)

* change owner and group
    

* create service file and add service file
    

* service file
    

=================

## 11/10/23

### Install TomCat..by khaja sir

[https://linuxize.com/post/how-to-install-tomcat-10-on-ubuntu-22-04/]

```bash
* tar
[https://linuxize.com/post/how-to-create-and-extract-archives-using-the-tar-command-in-linux/]
* wget
[https://linuxize.com/post/wget-command-examples/]
* symbolic link
[https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/]


* Manual steps....
```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat
# create user with following information
# username = tomcat
# group = tomcat
# homedir = /opt/tomcat
# shell = /bin/false
MAJOR_VERSION="10"
VERSION="10.1.14"
wget "https://dlcdn.apache.org/tomcat/tomcat-${MAJOR_VERSION}/v${VERSION}/bin/apache-tomcat-${VERSION}.tar.gz" -P /tmp
# download tomcat tar to /tmp
# file path: /tmp/apache-tomcat-10.1.14.tar.gz
sudo tar -xf /tmp/apache-tomcat-${VERSION}.tar.gz -C /opt/tomcat/
# extract tar file to /opt/tomcat
sudo ln -s /opt/tomcat/apache-tomcat-${VERSION} /opt/tomcat/latest
# Create a link for /opt/tomcat/apache-tomcat-10.1.14 to /opt/tomcat/latest
sudo chown -R tomcat: /opt/tomcat
# transfer of ownership to tomcat user
sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'
# Add execute permissions to all scripts in bin directory

# download tomcat tar to /tmp
# file path: /tmp/apache-tomcat-10.1.14.tar.gz
sudo tar -xf /tmp/apache-tomcat-${VERSION}.tar.gz -C /opt/tomcat/
# extract tar file to /opt/tomcat
sudo ln -s /opt/tomcat/apache-tomcat-${VERSION} /opt/tomcat/latest
# Create a link for /opt/tomcat/apache-tomcat-10.1.14 to /opt/tomcat/latest
sudo chown -R tomcat: /opt/tomcat
# transfer of ownership to tomcat user
sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'
# Add execute permissions to all scripts in bin directory
```

* Automation :-

```bash
# - name: install tomcat 10
#   become: yes
#   hosts: appservers
#   vars:
#     username: tomcat
#     groupname: tomcat
#     homedir: /opt/tomcat
#     shell: /bin/false
    tomcat_major_version: 10
    tomcat_specific_version: 10.1.14
    download_url: 
  # tasks:
  #   - name: install jdk
  #     ansible.builtin.apt:
  #       name: "openjdk-{{ java_version }}-jdk"
  #       update_cache: yes
  #       state: present
  #   - name: Ensure group "tomcat" exists
  #     ansible.builtin.group:
  #       name: "{{ groupname }}"
  #       state: present
  #   - name: create tomcat user
  #     ansible.builtin.user:
  #       name: "{{ username }}"
  #       group: "{{ groupname }}"
  #       home: "{{ homedir }}"
  #       create_home: true
  #       shell: "{{ shell }}"
    - name: Create a directory if it does not exist
      ansible.builtin.file:
        path: "{{ homedir }}"
        group: "{{ groupname }}"
        owner: "{{ username }}"
        state: directory
        mode: '0755'
    - name: download and extract tomcat
      ansible.builtin.unarchive:
        src: "https://dlcdn.apache.org/tomcat/tomcat-{{ tomcat_major_version }}/v{{ tomcat_specific_version }}/bin/apache-tomcat-{{ tomcat_specific_version }}.tar.gz"
        creates: "{{ homedir }}/apache-tomcat-{{ tomcat_specific_version }}"
        dest: "{{ homedir }}"
        group: "{{ groupname }}"
        owner: "{{ username }}"
        remote_src: true
    - name: Create a symbolic link
      ansible.builtin.file:
        src: "{{ homedir }}/apache-tomcat-{{ tomcat_specific_version }}"
        dest: "{{ homedir }}/latest"
        owner: "{{ username }}"
        group: "{{ groupname }}"
        state: link
    - name: Recursively change ownership of a directory
      ansible.builtin.file:
        path: "{{ homedir }}"
        state: directory
        recurse: yes
        owner: "{{ username }}"
        group: "{{ groupname }}"
    - name: get all the shell files
      ansible.builtin.command: sudo sh -c 'ls /opt/tomcat/latest/bin/*.sh'
      register: shell_files
    - name: print the value
      ansible.builtin.debug:
        var: shell_files
    - name: add execute permission
      ansible.builtin.file:
        path: "{{ item }}"
        owner: "{{ username }}"
        group: "{{ groupname }}"
        mode: "0751"
      loop: "{{ shell_files.stdout_lines }}"
```
