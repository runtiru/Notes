











## Class 26
## Ansible setup
[https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html]
    - create on ec2 instance (ubuntu)

apply those cammands on root user
    ^ sudo -i
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
    ^ cd /opt/
    ^ cat > hosts

    ^ vi hosts
add node private ip (jenkins-master)
```bash
[jenkins-master]
172.31.124.61

[jenkins-master:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/opt/rohitkey.pem
```
check the hosts file nodes are added are not
    ^ cat hosts
    ^ cd /home/ubuntu/
check the key 
    ^ ls
    ^ mv rohitkey.pem /opt/
    ^ cd /opt/
    ^ ls
    ^ ls -al
give file permitions
    ^ chmod 400 <keyneme> eg: rohith.pem
    ^ ansible all -i hosts -m ping
   yes
success

connect one more server (jenkins-slave)
    ^ vi hosts
```bash
[jenkins-slave]
172.31.124.61

[jenkins-slave:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/opt/rohitkey.pem
```
    ^ ansible all -i hosts -m ping
now both nodes are connet to the ansibel nade...


## 28 Class
### Setup jenkins using ansible



