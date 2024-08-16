# Ansible setup

* Create Master(controle) node instance..
    - Name: A_controle
    - OS `Ubuntu`
    - create new key pair `Acontrolekey.pem`  (controlekey.pem)
    - security group `Acontrole-SG`
        - ssh 22 allow form `MY IP` 
        - Lanch instances


* Create 3 server nodes 
    1. Web01 (vprofile-web01)
    2. Web02 (vprofile-web02)
    3. DB   (vprofile-db)

    - OS `Centos9` CentOS Stream 9(x86_64)
    - Instance type `T2.micro`
    - New Key `Anodeskey.pem`       (clintkey.pem)
    - SG `Anodes-SG`
        - ssh 22 allow form `MY IP`
    - Add onemore SG role
        - CustomeTCP 22 allow form Coustom source `Acontrole-SG`
    - Lanch instances

* Login controle node..
```sh
ssh -i ~/downloads`tab`\<key.pem> ubuntu@<IP>   ---> Both
```
* ssh (fingerprint)
    ^ ls ~/.ssh/know_host (/e/Users/imran/.ssh/know_hosts)
        - fingerprint are stre hear....
    ^ cat ~/.ssh/know_host or ^ cat ~/.ssh/authorized_keys


* Remove the fingerprint content (redirect the know_host)
    ^ cat /dev/null > ~/.ssh/konw_host 
    - now the file has empty

# Ansible Installation 
[https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html]
* Installing Ansible on specific operating systems
    * Installing Ansible on Ubuntu [https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu]

```sh
sudo apt update 
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y

ansible --version (ansible & Python)
```

===========

## Inventory
  
- it provide to basic information about ansible targets like ip address, username, password, keys, portnubers....

- two types to write inventory files

1. INI
2. Yaml (we use)

* ansible inventory (How to build your inventory)...?
[https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html]
    - default ansible inventory file `/etc/ansible/hosts`

* Login Controle instance

- create a folder `vprofile` ---> controle node

```sh
mkdir vprofile
cd vprofile
mkdir exercise1
cd exercise1
vim inventory
```

* Write invertory file with YAML

```sh
all:
  hosts:
    web01:
      ansible_host: <private ip of web01>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: Anodeskey.pem
```

save & quit (Ese :wq!)
    - exit Ec2
    - cat Downloads/Anodeskey.pem
copy the total key (becarefull)

login again the controle node..

  ^ cd vprofile/exercise1
    ^ ls (inventory)
    ^ cat inventory
    ^ vim Anodeskey.pem (clientkey.pem)
    - paste the total key data

* give a file permitions
    ^ ls -l (-rw-rw-r--  clintkey and inventory)
    <!-- ^ ansible web01 -m ping -i inventory -->

* create ansible configuration file
    - cd /vprofile/exercise1
    ^ sudo cat /etc/ansible/ansible.cfg
    - copy the command [ ansible-config init --disabled -t all > ansible.cfg ]

- switch to root user
    ^ sudo -i
    ^ cd /etc/ansible
    ^ ls [ansible.cfg]

- rename to this ansible.cfg 
    ^ mv ansible.cfg ansible.cfg_bakup
    ^ ansible-config init --disabled -t all > ansible.cfg
    ^ ls [ansible.cfg]
    - it's should be creat new ansible.cfg file

- edit this ansible.cfg file
    ^ vim ansible.cfg 
    - search for [:/host_key_checking=True]
    - remove the semecolon [ : ] or commit 
    - change host key checking true to False
    - save & quite [esc :wq!]
    - exit (logout)

```sh
cd /vprofile/exercise1 
pwd 
ls
ansible web01 -m ping -i inventory
```

  - if it error (failed to connect to the host via ssh)
  - git permmitions for A_Controlekey.pem (clientkey.pem)

```sh
chmod 400 Anodeskey.pem
ansible web01 -m ping -i inventory
```
success----

===========
## Inventory

- login clint node & copy exercise1 folder content to exercise2
    ^ cd vprofile
    ^ cp -r exercise1/ exercise2/
    ^ cd exercise2
- open the invertory file (exercise2)
    ^ vim exercise2

```sh
# all:
#   hosts:
#     web01:
#       ansible_host: <private ip of web01>
#       ansible_user: <ec2-user>
#       ansible_ssh_private_key_file: A_Controlekey.pem
    web02:
      ansible_host: <private ip of web02>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: A_Controlekey.pem
    db01:
      ansible_host: <private ip of db>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: A_Controlekey.pem
```
```sh
ansible web01 -m ping -i inventory
ansible web02 -m ping -i inventory
ansible db01 -m ping -i inventory
```

* if lot of invertory files are there we cont ping one by one lot of time her taken so we have Consept of GROPING.....

* Grouping:
  ^ vim inventory

```sh
all:
  hosts:
    web01:
      ansible_host: <private ip of web01>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: A_Controlekey.pem
    web02:
      ansible_host: <private ip of web02>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: A_Controlekey.pem
    db01:
      ansible_host: <private ip of db>
      ansible_user: <ec2-user>
      ansible_ssh_private_key_file: A_Controlekey.pem

  childern:
    webservers:
      hosts:
        web01
        web02
    dbservers:
      hosts:
        db01
    dc_oregon:  (parent group) (name of oregon you chose what you want)
      childern:
        webservers:
        dbservers:
```
```sh
ansible webservers -m ping -i inventory (only webservers)
ansible dbservers -m ping -i inventory  (only dbservers)
ansible dc_oregon -m ping -i inventory  (only dc_oregon servers)

ansible all -m ping -i inventory (all servers)
ansible '*' -m ping -i inventory (all servers)
ansible 'web*' -m ping -i inventory (only webservers start with web name)
```

* Now exercise2 copy to exercise
^ cp -r exercise2 exercise3
^ cd exercise3
^ ls (inventory)

* Variables
  . in exercise3
    ^ vim inventory

```sh
all:
  hosts:
    web01:
      ansible_host: <private ip of web01>
    web02:
      ansible_host: <private ip of web02>
    db01:
      ansible_host: <private ip of db>

  childern:
    webservers:
      hosts:
        web01
        web02
    dbservers:
      hosts:
        db01
    dc_oregon:  (parent group) (name of oregon you chose what you want)
      childern:
        webservers:
        dbservers:
      vars:
        ansible_user: <ec2-user>
        ansible_ssh_private_key_file: A_Controlekey.pem
```
```sh
ansible all -m ping -i inventory
```

===========
## YAML & JSON

# how to write a jenkins pipeline.?
