## 18/08/23
-----------
### Nopcommers installations  (manual steps)
--------------------------------------------
* create one ec2 instance (t2.medium - 20.04)
  web: nopcommers install on linux
refer: `install docker script`

  ^ sudo apt update
  ^  curl -fsSL https://get.docker.com -o install-docker.sh
  ^ sudo sh install-docker.sh
  ^ exit

  * dotnet-7.0
  ^ sudo apt update
sudo apt install snapd
  ^ sudo snap install dotnet-sdk --classic

    * java-17
  ^ sudo apt update
  ^ sudo apt install openjdk-17-jdk -y

  * cd /tmp/
  * wget https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip

  ^ sudo apt install unzip -y
  ^ mkdir bin cd ..
  ^ mkdir logs
  

  ^ unzip nopCommerce_4.60.2_NoSource_linux_x64.zip
  ^ dotnet Nop.Web.dll --urls "http://0.0.0.0:5000"
--------->
---xx----
    ^ wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    ^ sudo dpkg -i packages-microsoft-prod.deb

NOTE:- 20.04
  move to SDK or the .NET Runtime on Ubuntu
      move to Install .NET on Ubuntu 20.04

Bash:-
    ^ wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb

    ^  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-7.0

move to back (Install the .NET Core Runtime)
    ^ dotnet --list-runtimes
    ^ cd /tmp/
Get nopCommerce
:/tmp$ 
    ^ wget https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.4/nopCommerce_4.60.4_NoSource_linux_x64.zip

    ^  sudo apt-get install unzip -y
    ^ cp nopCommerce_4.60.4_NoSource_linux_x64.zip ~/nop
    ^ mkdir ~/nop
    ^ cd ~/nop/
    ^ unzip nopCommerce_4.60.4_NoSource_linux_x64.zip
    ^ mkdir bin
    ^ mkdir logs
    ^ dotnet /var/www/nopCommerce/Nop.Web.dll

    ^ dotnet Nop.Web.dll --urls "http://0.0.0.0:5000"

copy aws instance id - 
        web - paste id with :5000

-------
* create one ec2 instance (t2.medium - 20.04)
  web: nopcommers install on linux
need java 17
dotnet 7

 sudo apt update
 sudo apt install openjdk-17-jdk -y

  ^ wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb

  ^ sudo dpkg -i packages-microsoft-prod.deb
  ^ rm packages-microsoft-prod.deb

 sudo apt-get update && \
>   sudo apt-get install -y dotnet-sdk-7.0

  ^ java --version
  ^ dotnet --version
  ^ cd /tmp/
:/tmp$ 
  ^ git clone https://github.com/nopSolutions/nopCommerce.git

/tmp/nopCommerce$ 
  ^ dotnet restore src/NopCommerce.sln

/tmp/nopCommerce$ 
  ^ dotnet build -c Release src/NopCommerce.sln


## 20/08/23
-----------
### Docker Container Creation in docker playground:-
[refer:- class room notes]

## Installation of Docker Container in linux:-
--------------------------------------------
* update 
  ^ sudo apt update

* Docker installation - !Refer-[https://get.docker.com/]
    - 1. Download the script
  ^  curl -fsSL https://get.docker.com -o install-docker.sh
    - 2. Run the script either as root 
  ^  sudo sh install-docker.sh

* Information about docker
  ^ docker info    
      - hear run only Clint
      - we need to run Server also
  ^ sudo usermod -aG docker ubuntu

  ^ eixt (logout)
      and relogin 
  
  ^ docker info
      - now both Clint and Sever run
  
  
* Create a container
  ^ docker container run -d --name runner httpd
* List of containers
  ^ docker container ls -a

  ^ docker container run -d --neme runner2 -p 32000:80 httpd
  ^ docker container ls -a

  ^ history (what commands your using till now)
  ^ docker container run --name insteactice -d alpine
  ^ docker container ls -a
  ^ docker

* Container nameID only
  ^ docker container ls -a -q

* Remove container
  ^  docker container rm -f $(docker container ls -a -q)

* Remove Image
  ^ docker image rm -f $(docker image ls -q)


## 22/08/23
-----------
* How to know the process on your pc
    ^ ps aux
    ^ htop
    ^ ip addr
        link/loopback
        eth0 

* Mount partition in linux:-
  [refer:- notes]
# Creating Docker Container -----RT(23:30)
------------------------------------------
* login to docker 
    copy the docker ssh id and commet with APS

  ^ docker container run -it alpine /bin/sh

* check process tree --1
  ^ ps
      - prcess start with 1

* network interphase --2
  (/ # ifconfig) - in home directory
  ^ ifconfig 
      - 1. eth0 (Ethernet) - docker has own IP (172.17.0.2)
      - 2. lo (Loopback)

* parent machine
  ([node1] (local) root@192.168.0.28)
    ^$^ ifconfig
    - 1. eth0 (Ethernet) - docker parent machineIP (192.168.0.28)

* check the mounts in machine --3
 ^/#^ df -h

* As of now container is an isolated area which has its own
    process tree
    network interface
    file system
    users


## 23/08/23 
-----------
=================================================================================
-----------
# 24/08/23
-----------
# Install Docker with clint version and server vesion
-----------------------------------------------------
create on ec2 login to docekr 
(this is private key path - ssh -i ~/.ssh/id_rsa ubuntu@<id>) 

install docker - web: docker install script
  ^ curl -fsSL https://get.docker.com -o install-docker.sh
  ^ sudo sh install-docker.sh

add docker group in ubuntu
  ^ sudo usermod -aG docker ubuntu
  ^ exit and relogin

  ^ docker info / docker version

* create one container 
  ^ docker container run -d --name <name> nginx
  ^ docker container ls / docker image ls
  ^ sudo apt update && sudo apt install openjdk-11-jdk -y
  ^ docker info

# Maual stepts for spc:-
* create an ubuntu instance and login into that <springpetclinic>
* install jdk-11
  ^ sudo apt update && sudo apt install openjdk-11-jdk -y
  ^ java -version

* download the application
  ^ cd /tmp/
  ^ wget https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar
  ^ ls
  [springpetclintc-2.4.2.jar]

* Now to run the application  ----------------->RT (25:35)
  ^ java -jar /tmp/spring-petclinic-2.4.2.jar

* Now access the application 
    [http://<public-ip>:8080]

# Nginx
  ^ docker container run -d --name mynginx -p 44444:80 nginx

  * create an container:-
    ^ docker container run -it -p 33333:8080 openjdk:11 / bin/badh
  * goto to inside the container 
    ^ docker container exec -it 9492e081c466 bash

## Building Docker Image:-    ----------RT(57:30)

create ec2 and login docker 

  ^ vi Dockerfile --> (need D cap-lt)
----------
FROM openjdk:11   --> (what are requrd)
ADD wget https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar
EXPOSE 8080
CMD ["java", "-jar", "/springpetclinic-2.4.2.jar"]
----------
  ^ Esc :wq!
  ^ docker image build -t spc:1.0 .    --> (. is needed)
sucess
  ^ docker image ls
spc 1.0

* Build again
  ^ docker image build -t spc:1.1 .   --> (. is needed)
  
  ^ docker container run -d --name spc -P spc:1.0 
  ^ docker container ls
now copy the instance id and paste the new web
ex: [35.160.24.177:32768]
--run thr spc--

* create onemore container 
  ^ docker container run -d --name spc1 -P spc:1.0
now 2 containers are running

    ^ docker stats   (container deep view)

* create onemore container 
  ^ docker container run -d --name spc2 -P spc:1.0
now 3 containers are running

  ^ htop   (show the CPU, Mem conseption)

=================================================================================
## 25/08/23
------------
# Activitie
-----------
  * Create a linux instance and install docker in it.

  * Create a container with name myhttpd1 and image httpd.
      ^ docker container run --name myhttpd1 -d httpd

  * Create a container with name myhttpd2 and image httpd and forwarding 80 port of the container to 32000 port of the linux vm.
      ^ docker container run --name myhttpd2 -p 32000:80 -d httpd
  
  * Create a container with name interactive and image alpine.
     ^ docker container run --name interactive -d alpine

  * Verify the containers which are running..?
     ^ docker container ls -a

  * myhttpd1 and myhttpd2 will be in running state and interactive will be in exited state.

* Remove all the containers 
  ^ docker container rm -a       ---------> all the containers info
  ^ docker container rm -a -q    ---------> all the containers id's only
  ^ docker container rm -f $(docker contaienr ls -a -q)  ------> delete all the containers
  ^ docker image ls -q           ---------> all the images
  ^ docker image rm -f $(docker image ls -q)  -----> delete all the images


* Lets create a container and login into that during running the container. Lets use alpine and ubuntu docker images.
  ^ docker container run -it --name alpine alpine /bin/sh  ----> container create and go to inside the container.

  ^ whoami    -----> (where is the container - root /)

* Exit
  ^ [contrle + pq] or [controle + d]

* create ubuntu contianer 
  ^ docker container run -it --name ubuntu01 ubuntu /bin/bash
  ^ whoami

# how to go inside the container:- -----> RT (54:50)
  ^ docker container exec nginx01 whoaim
  ^ ls -al /bin/


  ^ docker container exec -it nginx01 /bin/bash

# Docker container can be executed in 3 ways
    1. detached
    2. attached
    3. interactive

* Lets create the nginx container in "detached" mode [-d]
  ^ docker container run -d --name nginx01 nginx
  ^ docker container ls 

* Lets create the nginx container in "attached" mode
  ^ docker container run --name nginxa nginx

===========================================================================
## 26/08/23 - AWS Docker with K8s
---------------------------------
### Interactiog with containers
--------------------------------
* create on ec2 and login into docker 
        creatate a container      ------> 
  ^ docker container run -it --name 
        login into that container --> 
  ^ docker container exec -it nginx01 /bin/bash
now inside the container .......
--->
* Don't run your container with intrractive mood
  ^ docker container run --name interactive -it nginx /bin/bash
  ^ ls /usr/share/
exit ---
  ^ docker container ls ----> the container was not running now...!
[NOTE: never start the container in interactive mood]

* Run your container in detached mood
  ^ docker container run --name detached -d -P nginx
  ^ docker container exec -it detached /bin/bash
  ^ ls /usr/share/
exit ---
  ^ docker container ls ----> the container is running now
--->

### Containerization using dockerfile:-
---------------------------------------
[refer for class notes]

* Alias
-------
linux alias command 
    ^ alias CD="cd Desktop"

command line delete
  ^ docker container rm -f $(docker container ls -a -q)

Alias
  ^ alias rmdc="docker container rm -f $(docker contianer ls -a -q)"

  ^ alias rmi="docker image rm -f $(docker image ls -q)"
* Use alias -------RT (08:45)
    ^ vi ~/.bashrc (ec2 instance)
inside vi add this files
  - alias rmi='docker image rm -f `docker image ls -q`'
  - alias rmc='docker container rm -f `docker container ls -a -q`'
    ^ source ~/.bashrc
    ^ rmc 

============================================================================
## 26/08/23 - TERRAFORM WORKSHOP
--------------------------------
  # Activities
      * Create the network
      * Create the database
      * Optional: Create a vmimage/ami (manually)
      * Create the vm/ec2 instance in subnet
      * Execute provisioning
           - terraform => provisioner
           - arm templates/bicep => extension or user data
           - cloudformation => userdata
           
============================================================================
## 27/08/23
-----------
goto inside of the container 
  ^ decker container run -it <amazoncorretto:11-alpine3.17> /bin/sh 
      [hear /sh - alpine is slime version]
      [you have a large version you can give /bash]
  
* how to give groupadd
after going to inside the container 
` / ` - root user
  ^ / # groupadd --help
not found
  ^ / # useradd --help
not found
[heat no group and no user]
  ^ / # adduser --help
-h [DIR] Home directory
-s [SHELL] Login shell
-G [GRP] Group
-D Don't assign a password 
-u [UID] User ID

  ^ / # ls
some folders are available
bin   home    media   lib ...........!

  ^ / # adduser -h /petclinic -S /bin/sh -D petclinc
[/ # adduser '-h /<name of the work directory> eg:- petclinic' -S <create a group> /bin/sh -D <no passwd> petclinc <username>]

  ^ cat /etc/passwd
now show the petclinc user [/petclinc:/bin/sh]

  ^ / # ls -al
now seen petclinc <user/group>
      [OR]
  ^ $ cat /etc/group
  ^ $ pwd

  # Activities
    * Simple:
        Gameoflife application:
            requires:
              jdk8
              tomcat 8 or 9
              Copy the war file into webapps folder of tomcat 9
              Access the application by <tomcat-url>/gameoflife

    * Tricky: Refer Here for nopCommerce on Linux
    Note: dont focus on database, configure the rest.

======================================================================
## 29/08/23
-----------
### Gameoflife application:-
  * JDK-8
  * Tomcat 8 or 9

create ec2 login to docker (docker install scriept)
  ^ curl -fsSL https://get.docker.com -o install-docker.sh
  ^ sudo sh install-docker.sh

  
  ^ docker container run -d -P --name manual tomcat:9-jdk8


-----
======================================================================
## 31/08/23
-----------
