# Project:1

Create EC2 instances

1. Jenkins-Server
2. Sonar-Server
3. Kops (Kubernetes)
4. DockerHub

 <!-- Nexus-Server -->  (Optional)

## Jenkins-Server SetUp

Create VM for jenkins (Jenkins-Server)
        New Key pair (Jenkins-key)
        New Security group (Jenkine-SGN)
        - Inbound Security Group Rules - SSH & My Ip
                                        - Custom TCP (8080) & AnyWare

Login VM & Root user

```sh
#!/bin/bash
^ sudo apt update
^ sudo apt install openjdk-17-jdk -y

^ curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

^ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

^ sudo apt-get update
^ sudo apt-get install jenkins -y

^ systemctl status jenkins
^ id jenkins
```

Login jenkins-server new window (public ip:8080)
   now copy the '/var/lib/jenkins/secrets/initialAdminPassword'
   cat /var/lib/jenkins/secrets/initialAdminPassword  (this is the root user no need to sudo)
   copy the passed : 5347d64abf684001a49b4693ada8815d

   Create First Admin User:
        username: admin
        Password: admin123
        Confirm password: admin123
        Full name: not prefer
        E-mail address: not prefer

Instance Configuration:
     `http://44.200.246.211:8080/`  -  This is jenkins URL (here once power of the vm the IP will change so better to give the domain name URL (gmail), domain never change anyware)
     Eg: `http://admin.mydevops.xyz/`

start using jenkins now......

* Jenkins URL Settings
If you want to change jenkins URL
  - Goto Manage jenkins - systerm - jenkins location (jenkins URL)

==================================================================

## Sonar-Server SetUp

Create EC2 for Sonarqube (Sonar-Server)
        New Key pair (Sonar-key)
        New Security group (Sonar-SGN)
        - Inbound Security Group Rules - SSH & My Ip
                                        - Custom TCP (80) & AnyWare
                                        - Custom TCP (80) & Coustom (Jenkine-SGN - Allow jenkins to sonar)
        Advanced details
         - User data - optional
           open github - vprofile-project/userdata/sonar-setup.sh
           copy the data & paste data to advanced details...

```bash
#!/bin/bash
cp /etc/sysctl.conf /root/sysctl.conf_backup
cat <<EOT> /etc/sysctl.conf
vm.max_map_count=262144
fs.file-max=65536
ulimit -n 65536
ulimit -u 4096
EOT
cp /etc/security/limits.conf /root/sec_limit.conf_backup
cat <<EOT> /etc/security/limits.conf
sonarqube   -   nofile   65536
sonarqube   -   nproc    409
EOT

sudo apt-get update -y
sudo apt-get install openjdk-11-jdk -y
sudo update-alternatives --config java

java -version

sudo apt update
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
sudo apt install postgresql postgresql-contrib -y
#sudo -u postgres psql -c "SELECT version();"
sudo systemctl enable postgresql.service
sudo systemctl start  postgresql.service
sudo echo "postgres:admin123" | chpasswd
runuser -l postgres -c "createuser sonar"
sudo -i -u postgres psql -c "ALTER USER sonar WITH ENCRYPTED PASSWORD 'admin123';"
sudo -i -u postgres psql -c "CREATE DATABASE sonarqube OWNER sonar;"
sudo -i -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;"
systemctl restart  postgresql
#systemctl status -l   postgresql
netstat -tulpena | grep postgres
sudo mkdir -p /sonarqube/
cd /sonarqube/
sudo curl -O https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.3.0.34182.zip
sudo apt-get install zip -y
sudo unzip -o sonarqube-8.3.0.34182.zip -d /opt/
sudo mv /opt/sonarqube-8.3.0.34182/ /opt/sonarqube
sudo groupadd sonar
sudo useradd -c "SonarQube - User" -d /opt/sonarqube/ -g sonar sonar
sudo chown sonar:sonar /opt/sonarqube/ -R
cp /opt/sonarqube/conf/sonar.properties /root/sonar.properties_backup
cat <<EOT> /opt/sonarqube/conf/sonar.properties
sonar.jdbc.username=sonar
sonar.jdbc.password=admin123
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
sonar.web.host=0.0.0.0
sonar.web.port=9000
sonar.web.javaAdditionalOpts=-server
sonar.search.javaOpts=-Xmx512m -Xms512m -XX:+HeapDumpOnOutOfMemoryError
sonar.log.level=INFO
sonar.path.logs=logs
EOT

cat <<EOT> /etc/systemd/system/sonarqube.service
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop

User=sonar
Group=sonar
Restart=always

LimitNOFILE=65536
LimitNPROC=4096


[Install]
WantedBy=multi-user.target
EOT

systemctl daemon-reload
systemctl enable sonarqube.service
#systemctl start sonarqube.service
#systemctl status -l sonarqube.service
apt-get install nginx -y
rm -rf /etc/nginx/sites-enabled/default
rm -rf /etc/nginx/sites-available/default
cat <<EOT> /etc/nginx/sites-available/sonarqube
server{
    listen      80;
    server_name sonarqube.groophy.in;

    access_log  /var/log/nginx/sonar.access.log;
    error_log   /var/log/nginx/sonar.error.log;

    proxy_buffers 16 64k;
    proxy_buffer_size 128k;

    location / {
        proxy_pass  http://127.0.0.1:9000;
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_redirect off;
              
        proxy_set_header    Host            \$host;
        proxy_set_header    X-Real-IP       \$remote_addr;
        proxy_set_header    X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header    X-Forwarded-Proto http;
    }
}
EOT
ln -s /etc/nginx/sites-available/sonarqube /etc/nginx/sites-enabled/sonarqube
systemctl enable nginx.service
#systemctl restart nginx.service
sudo ufw allow 80,9000,9001/tcp

echo "System reboot in 30 sec"
sleep 30
reboot
```

Lanch Instance now...
 - login the EC2 instance

```sh
^ ssh -i Downloads/sonar-key ubuntu@IP_address (public IP)
```

 open web browser and paste the public IP of sonar instance id (3.85.50.70)

LogIn to sonar 
   usernaem: admin
   passwd: admin
(you can restart any time)
------------------------------

* Login jenkins & sonarqube servers
      in sonarqube jenerate a new token for connect to jenkins..

* Create Token
   open sonarqube administrator and goto security - Generate token 
   - Give a name and generate (copy the token and keep it safe)

Open jenkins - Manage jenkins - Credentials - System - Global credentials (unrestricted)
  Name of the sonar token (sonar-pro) - Server URL (private ip of sonar server - `http://172.31.7.31`) - add the token 

Add credentials
     Domain: Global Credentials (unrestricted)
     Kind: Secret text
       - Scope: Global (jenkins, nodes, items,....)
       - Secret: paste the sonar secret token (keep it safely)
       - ID: kube-sonar-token (as your wish)
       - Description: kube-sonar-token

select the server authountication token - kube-sonar-token

seve settings...

Now goto jenkins ce2 to allow securty connection for sonarqube server

jenkins ce2 open security settings, add inbond rules - add rule - (all traffic : sonar-sgn) - save

check sonar security if the jenkins security is connect or not...?
sonar ce2 open security settings, add inbond rules - add rule - (all traffic : sonar-sgn) - save

====================================================================

## 4.Docker Hub

* In jenkins add dockerhub credentials
   Dashboard - Manage Jenkins - Credentials - System - Global credentials (unrestricted)

Login jenkins-server and install docker installation script on jenkins server ([install docker engine on ubuntu](https://docs.docker.com/engine/install/ubuntu/))...

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl status jenkins
sudo usermod -aG docker jenkins
sudo docker images
restart the machine
```

* Now install the plugins on jenkins...
   Dashboard - Manage Jenkins - Plugins - available plugins
   . docker
   . docker pipeline
   . pipeline utility steps
  install without restart....

================================================================

## 3. Kops (Kubernetes) - SetUp

Create EC2 for Kubernetes (Kops)
   - New Key pair (Kops-key)
   - New Security group (Kops-SGN)
      - Inbound Security Group Rules - SSH & My Ip

- Now Create Kubernetes cluster:
   useing Kops command (note - Kops is not part of k8s cluster)

- Before create cluster we need some requirments...
   - S3 Bucket
   - Route 53
   - Iam user

# Create S3 bucket

   - General configuration
      - AWS Region - US East (N. Virginia) us-east-1
      - Bucket type - General purpose
      - Bucket name - udemy-bucket-n

   - Object Ownership
      - ACLs disabled (recommended)
   
   - Block Public Access settings for this bucket
      - (ok) Block all public access
      
 Create bucket...


# Create IAM
------------
   - IAM Dashboard (IAM - Users - Create user)
      - Name: kopsadmin (next)
      - Attach policies directly
         - AdministratorAccess (next)
   create user....

Open the user
   - Security credentials
      - Access key
         - Create access key
            - Command Line Interface (CLI) - Confirmation (OK) - (next)
   Create access key....

(Download .csv file) - Done..

# Create Route 53

Route 53 Dashboard
   - Create hosted zone
   - Hosted zone configuration
      - Domain name: kubevpro.groophy.in (ram.runtiru.xyz)
      - Description optional: 
      - Type - Public hosted zone
   Created Hosted zone....

   - Goto GooDaddy account
      - Domain Portfolio - DNS - Add New Record - Type (NS: Nameserver)

add like this to "Route 53 to Goodaddy"
   NS - kubevpro - ns-1458.awsdns-54.org.  (NS - ram - ns-1458.awsdns-54.org. )
   NS - kubevpro - ns-381.awsdns-47.com.
   NS - kubevpro - ns-1855.awsdns-39.co.uk.
   NS - kubevpro - ns-569.awsdns-07.net.

* Now login to kops EC2
   - Generate ssh-key " ^ssh-keygen"
   - Install AWSCLI (choco install awscli)
```bash
sudo apt update

1. (curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install)

2. (sudo apt install unzip)

3. (curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install)

aws console (sudo apt install awscli -y)
aws configure
   - add the access key & secret key
   - region
   - name (not required)

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

ls
sudo chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

web - Install and Set Up kubectl on Linux 
[https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/]

* Install kubectl binary with curl on Linux
   - Download the latest release with the command:
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

ls 
chmod +x ./kubectl
sudo mv kubectl /usr/local/bin
kubectl --hepl (conform kubectl install or not)
```
# Install kops (Old versin - v1.26.4)
--------------
   - https://github.com/kubernetes/kops/releases?page=3
   - v1.26.4
   - Assets "kops-linux-amd64" - copy the link (dont download manully)

In Kops - EC2 instance wget the copy link
```bash
wget https://github.com/kubernetes/kops/releases/download/v1.26.4/kops-linux-amd64

ls (kops-linux-amd64)
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops
kops version (v1.26.4)
```

* Now verfy the domain
```bash
nslookup -type=ns kubevpro.groophy.in (ram.runtiru.xyz)
```
(4 name server on visible)
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
ram.runtiru.xyz nameserver = ns-904.awsdns-49.net.
ram.runtiru.xyz nameserver = ns-1231.awsdns-25.org.
ram.runtiru.xyz nameserver = ns-2023.awsdns-60.co.uk.
ram.runtiru.xyz nameserver = ns-441.awsdns-55.com.
-------

# Create kubernetes cluster
   - Run Kops command to created kubernetes cluster..
```sh
# kops create cluster --name=kubevpro.groophy.in \ 
# > --state=s3://vprofile-kop-states --zone=us-east-2a, us-east-2b \
# > --nede-count=2 --node-size=t3.small --master-size=t3.medium --dns-zone=kubevpro.groophy.in \
# > --node-volume-size=8 --master-volume-size=8
```

```bash
 kops create cluster --name=ram.runtiru.xyz --state=s3://udemy-bucket-n --zones=us-east-1a,us-east-1b --node-count=2 --node-size=t2.micro --master-size=t2.medium --dns-zone=ram.runtiru.xyz --node-volume-size=8 --master-volume-size=8
```

```bash
kops update cluster --name runtiru.xyz --state=s3://udemy-bucket-n --yes
```

```bash
kops validate cluster --state=s3://udemy-bucket-n 

kubectl get nodes
```
* Delete cluster..
```sh
 kops delete cluster --name=ram.runtiru.xyz --state=s3://udemy-bucket-n --yes
```


# Install HELM.. 
([Helm.sh](https://helm.sh/))
   - Get started
   - Install Helm - the installation guide.
   - From the Binary Releases
      - desired version
         - Helm v3.15.1 (Latest) - github
            - Linux amd64 (https://get.helm.sh/helm-v3.15.1-linux-amd64.tar.gz)
   (downlod locally & copy the link)

```sh
cd /tmp/
wget https://get.helm.sh/helm-v3.15.1-linux-amd64.tar.gz
tar xzvf helm-v3.15.1-linux-amd64.tar.gz
cd linux-amd64/
ls
sudo mv helm /usr/local/bin/helm

kubectl get nodes


==============





yg








