# 04/10/23
----------
## User Creation
* ssh (scure Shell):- 
    - is a network protocol used for secure remote access to computer systems over a potentially unsecured network.

* Linux:-
    - linux is a kernel 

* Kernel:-
    - core oprating system which capability speake whith hardware giveing simple interphase

* Distubuations
* Shell

Debian Family
    - Ubuntu
    - Kali
    - Debian

Redhat Family
    - Redhat
    - Fedora
    - Centos
    - RHEL
    - Amazon Linux

* username
 
* public key
* public IPv4 address

* private key
* private IPv4 address

* RSA
* .pem
* ssh servier
* ssh clint

* sftp (SSH file tranfer protocal)
Changing file permissions
* chmod 400

* sftp
* vi
* systemctl
adduser
    
================================================================== 
## 05/10/23
-----------
[https://directdevops.blog/2023/10/05/devops-classroomnotes-05-oct-2023/]
## Create a user and
## Setting up password less authentication between linux machines:-

* Create 2 instances
    server-1 and server-2
    login that matchane 
    ^ ssh -i ~/downloads`tab`\<key.pem> ubuntu@<IP>   --->2

  - passwd authuntication yes
    ^ sudo vi(nano) /etc/ssh/sshd_config  ---2
  PasswordAuthentication `yes`
   `Esc:wq!`

  - restaer the server
  ^ sudo systermctl restart sshd    ---2

  - create user 
  ^ sudo adduser devops ----2
  Password:<runner>

  - communicate with 2 servers
  ^ ssh devops@<private ip of server2>  ---(1)
    Password: *****
  ^ exit

# Adding user to sudo    ------>RT (14:00)
  - Adding user to sudo     ----2
  ^ sudo visudo
  In %sudo-->
  devops ALL=(ALL:ALL) NOPASSWD:ALL
<!-- Ctrl+o
        enter
          ctrl+x -->

  - switch user     ---2 
  ^ su devops
  passwd ****
  
  - home directory      ---2
    ^ cd ~
    ^ pwd
    /home/devops

    ^ sudo apt update   ---2

<!--
    * login form one server to another server   ----->RT (21:00)
      ^ ssh <private ip server2>  ---(1)  
   <!-- Password: *****
    ^ eixt  
    -->
 
# setting password less authountication in server1 and 2   

* create key pair in sercer1    ---(1)
    ^ ssh-keygen 
  - check the both keys
    ^ ls ~/.ssh/
  id_rsa   id_rsa.pub   known_hosta   
  <!-- - ~/.ssh/id_rsa   ==> private key
       - ~/.ssh/id_rsa.pub ==> public key -->

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
    ^ ssh-copy-id devops@<private ip2>
   password:******
---xx---
In server2
    ^ ls ~/.ssh/
  authorized_keys = (private of server1)
    ^ cat ~/.ssh/authorized_keys 
---xx---
* After the ssh-copy-id is success, then we can login directly by using ip address as both machines have same username and password less authentication is setup.
* switch to one server to another server
<!-- 
    In server1
    ^ ssh <ip adderss of server2>
  server1 changed to servewr2
    ^ exit 
    -->

----------------------------------------

## Ansible setup:-
   - we have two machines with common user devops
   - sudo permissions and password less authentication setup between server 1 and server 2
   - From now server 1 will be called as `Ansible Control node`
and server 2 as `node 1`

* Ensure python:3 is installed
    ^ python3 --version     ------2
   Python 3.10.6
<!-- * :- If python is not installed `install pythone on ubuntu` -->
`Installing and upgrading Ansible with pip`
[https://docs.ansible.com/ansible/latest/installation_guide/index.html]

# Install ansible      -----RT (35:00)
[https://docs.ansible.com/ansible/latest/installation_guide/index.html]
* We have two approaches to install ansible
    Debian --> apt 
    RedHet --> yam (dnf)

Debian:-
   - apply those commands on server1 -----(1)
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```
    ^ ansible --version
  ansible [core 2.15.4]

## Test ansible connectivity from ansible `control node` to `node1`
* Create a file with node 1 ip address in it
  - Create a file 
    ^ echo <Ip address-2> > hosts
    ^ cat hosts
  172.31.17.52

* execute the following command `ansible -m ping -i hosts all`
    ^ ansible -m ping -i hosts all
<---SUCCESS--->
-----------------------------------------------------

* Changing the host     ---->RT (46:00)
    ^ vi hosts    ----(1)
        172.31.17.52
        (localhost)
        
    ^ ansible -m ping -i hosts all
Its dosent move `-X-`

    ^ ssh-copy-id localhost
   Password:*****

    ^ ansible -m ping -i hosts all
<---SUCCESS--->

    ^ ansible --help | less (more)
* connect to ansible ----(1)
    ^ ansible -i hosts -u devops -K -m ping all
   Password: ******
<---SUCCESS--->

* Ansible can communicte other machine useing two ways:-
    - key based authountication
    - password based authountication

==================================================================
## 06/10/23
### YAML





