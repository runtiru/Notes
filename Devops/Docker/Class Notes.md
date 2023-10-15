## 18/08/23
-----------
### Bringing up the Application to sell products online:-
----------------------------------------------------------
* (Bringup one Ecommers appliaction - nopcommers)


* Continues Deliviry/Deployment

Devolopers---> code(VCS)--> Build/Package---> Systemtest(St-E)---> Perfomes(Pt-E)---> UAT/Pre-prod---> Production Env
                Git          maven,             Terraform,         automated tests
                Github       Ms Build,          Ansible,           process results
                             Docker             Kubernites
# CI/CD
    * jenkins
    * Azure DevOps
    * GitHub Actions

* Do you have a servers...?
    - Yes
       - Linux/Windows servers ==> Ansible(Configuration managment)
       - Containers ==> Kubernetes (OLD)

    - No
       - Terraform (infra provisioning) - severs

# Micreosevices Arct
--------------------
# Ecommerce
* User Managment 
    - create an users and reset passwd to usrs
    - ability to create an users

* Catalog (iteams)
    - the hole set of iteams we are selling on ecommers

* Cart Management
    - add to iteams

* Order Management
    
* Payment Services

=================================================================
## 19/08/23
-----------
### Application Deploymet - Generation Wise
-------------------------------------------
      application
       platform
          OS
         SEVER 

* Capex (capital expenditure):- (INVESTMENT)
    - The investment whitch you do before your application deployed 

    - funds used by a company to acquire, upgrade, and maintain physical assets such as property, plants, buildings, technology, or equipment.
  
* OpEx (Opration expenditure):- (monthly expenditure)
    - the money a company or organization spends on an ongoing, day-to-day basis to run its business

# Gen-2:-
* Hypervisor (VM Ware)
    - Software that creates and runs virtual machines (VMs).
    - You can useing one system and you create number of VM's inside your system
    - The hypervisor creates multiple vm's
    - Hypervisers creates isolations.

* Isolations:-
    - isolation create own space to run an OS.

# Introduce our first character PHIPPY:-
---------------------------------------
    - Phippy is a simple single page PHP application ()
    - 
# What is KUBERNETES (K8s)..?
    - An open-source system fot automating deployment, scaling, and management of containerized appliction
    - 
### What is DOCKER...?
----------------------
* ![Priview] https://www.youtube.com/watch?v=wW9CAH9nSLs

    - Docket was inially disign for linux 
    in that linux one technology LXC (Linux containers) 
[ Docker was use to LXC, and this lxc was create Container.]

Clint side appliction
Severs side appliction

* PaaS - Plateform as a service 

* What is Docker do...?
    - Docker lets you build, test, and deploy applications quickly

=================================================================
## 20/08/23
-----------
### Docker Container Creation:-
-------------------------------
* Create a DockerHub Account - https://hub.docker.com/signup
* Navigate to Docker playground - https://labs.play-with-docker.com/

When you install a Docker -
    * Docker have  two major components
        1. Docker client:-
            - it's is a command line we will be using.
            - 
        2. Docker engine (server/daemon)
            - local repo

to run an a container(after installation)  ----RT(27:00)
    ^ docker container run hello-world - unable to find
    ^ docker container run hello-world

* To create container user has to execute docker container run <image>

* docker daemon will received this request and checks if the image is present locally.

* If it is not present, it downloads from registry (default registry is docker hub)

* One image is present then the container is created.


## 22/08/23
-----------
### What dose docker container provide...?
------------------------------------------
* Every application needs:-
    - process to execute to CPU and RAM.
    - network interface for accessing the application.
    - storage or mount space will have OS.

* As of now container is an isolated area which has its own
        process tree
        network interface
        file system
        users
   
* Every application as a process
    * What ever your thinking as an application your os deels that an process
        Eg:- Tomcat
            Apache ,
* PID is the first prossecer for your first machine.

* local host:-  
    - LH is always your computer
    - on computer networking,  localhost is a hostname that refers to the current computer used to access it.

    [http://loclahost:8080 / http://127.0.0.1:8080]


* Linux filesystem hierarchy standard (FHS)
    - a reference describing the conventions used for the layout of a UNIX system.

* Mount partition in liux
-------------------------
    - a directory where an external partition, storage device, or file system can become accessible to the user or application requiring it.

# Windows vs Linux
------------------
* Microsoft windows
    - Microsoft is a commercial opraitong system 
    - Windows is generally considered to be easier to use.

* Linux
    - its an OS
    - Linux is known for its stability and security.


# Types of docker
![preview](image.png)
# Differnce between local host vs docker host
* Local host
* Docker host
    - Docker container starts with " / " - (root /)
    
![preiview](image-1.png)
---
            create               create
Docker file ------> Docker image -------> Docker container
---

* after create a container is an isolated area which has its own
        process tree
        network interface
        file system
        users

# How are these created:-
Linux OS has tow areas
    A. Namespaces
    B. Controle groups

A. Namespace:-
-------------
  - Namespaces created isolations
  - isolations are created with the help of namespaces
  the limitations or restrictions on isolated areas can be acheive using control groups.

    1. Process namespace (PID) - process isolation
        - its create a new process into a container. (your system injected new process)
        - it's start with process ID-1
        - associated with CPU and RAM

    2. Mount namespace (MNT) 
        - / (root) 
        - create a file system, all the content in that file (OS)

    2. Net namespace - network istolation
        - its created 2 network interphases 
                - eth0 (Ethernet) 
                - lo (Loopback)
                
    3. User namespace (url) new set of your pc
        - It's created new set of user

B. Controle groups:-
--------------------
    - it's created on Limitations or Rrstrictions
    - The limitations or restrictions on isolated areas can be acheived using control groups

-----

* LXC (linux container):-
    - part of linux and it create containers 
    - it's a part of linux kernel releases

* Libcontiner:-
    - it's created low level component 

* Docker Internals:-
!Refer Here (https://directdevops.blog/2019/01/31/docker-internals/)

* What is the docker..?
    - Docker is an isolated area, contaienr is an isolated area and 
    into that isolated are it will have its own CPU and Memory, Network interphase.
(in isolated areas created namespaces)
    - docker to your syserm in a process, docker have containers , inside a container  an OS is present.

* K8s does not support docker:
    - Kubernetes is removing support fot Docker as a container runtime..
    - K8s does not actually handle the process of running containers on a machine. Instead, it relies on another piece of software called a container runtime.
    - containers give varchual OS
        in that varchual os have 
                - V.CPU, V.HD, V.RAM, V.Memory
    - Varchual machine create - V.CPU, V.HD, V.RAM, V.Memory
                those are all create V.OS
=================================================================================
## 23/08/23 
-----------
### Standards in containers
---------------------------
## Docker Architecture
-----------------------
* Docker have  two major components
    1. Docker engine (server/daemon)
        - local repo
    2. Docker client:-
        - it's is a command line.
    
- when your enter any command in docker(clint) -----> docker clint speak with docker sever ..
- docker was use to run microservices.

- docker its self monolithic application. (first services) 

* OCI (Open Container Initative)
    - two differnt companys try to buid the containers in two differnt ways.
    - a collaborative project hosted under the Linux Foundation that is designed to establish common standards for container formats and runtimes.

* Daemon:- in docker
    - Daemon is a lightwight component 
    - Docker daemon is a persistent background process that manages the containers on a single host.
    - forword a information of create a container into containerD

* ContainerD:-
    - Daemon says to create container
    - implimentation of OCI
    - how to manage images and how to speake images.
    - a Docker-developed container runtime that manages the life cycle of a container on a physical or virtual machine.

* RunC
    - it's create docker container.
    - a lightweight, portable container runtime.
    - implimet our one time.
    - libcontainer part of runC

* Shim:-
    - shim is a parent of a container
    - once the contianer is created runc makes shim the parent of cintainer, this helps docker 

## Dockcer container lifecycle
------------------------------
           create               create
Docker file ------> Docker image -------> Docker container

## Docker installation (linux)
------------------------------
* create an instance (ec2-ubuntu 22.)
    
^ curl -fsSL https://get.docker.com -o install-docker.sh

^ sudo sh install-docker.sh

=================================================================================
-----------
# 24/08/23
-----------
# Install Docker
(ssh -i ~/.ssh ubuntu@)

* Base image:- the image that is used to create all of your container images.

* Containerization:-
    - This is the process of running the application in containers.
    - This majorly means creating a Dockerfile for every application developed by your dev team.

* Port forwarding:-
    - allows you to expose container ports to the outside world. 

* Case-Study: spring petclinic:-
    - This is a sample java application
    - To run this application we need java 11 and 8080 port to access the application.
    - 
your work in an organization 
  - sit with the developer and figure out the how the application id exicterded, what is requried for the application, what are configaration which we do...?

# Docker Image information -------------RT(33:00)
    * Docker hub has 3 types of images
        1. official images
        2. Verified Publisher
        3. Community Images

    * Registries like DockerHub have repositories.
    * Each Docker Image will have a Repository
    * Docker image name convention
----
# for non official images
<username>/<repository>:<tag>
# for offical images
<repository>:<tag>
----
 
## Building Docker Image:-    ----------RT(57:30)
--------------------------
    * Choose the right base image
    * Composing a Dockerfile

=================================================================================
## 25/08/23
------------
# Activitie
-----------
  * Create a linux instance and install docker in it.

  * Create a container with name myhttpd1 and image httpd.

  * Create a container with name myhttpd2 and image httpd and forwarding 80 port of the container to 32000 port of the linux vm.
  
  * Create a container with name interactive and image alpine.

  * Verify the containers which are running..?

  * myhttpd1 and myhttpd2 will be in running state and interactive will be in exited state.

## Observations
    Not all the containers when executed will be in running state. the alpine container with the name interactive went into exited state.

* Docker container can be executed in 3 ways
        detached
        attached
        interactive

===========================================================================
## 26/08/23 
-----------
### Containerization using dockerfile:-
---------------------------------------
    - Dockerfile is a set of instructions which help in building the docker image.

Alias:-

# Dockerfile:-
-------------
1. FROM amazoncorretto:11 (what is your flatform type):(tag)
2. LABEL author="khaja" (adds metadata to an image)
3. LABEL orgnaization="learningthoughts" (<key>=<value>)
4. RUN wget https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar  (execute instructions for configuring your application)
5. EXPOSE 8080 (expose container ports)
6. CMD [---]   (run the command during startup)



^ socker container run -it amazoncorretto:11 /bin/bash

----
* Expose: expose container ports
how to know docker port 80 run

docker container run -d -p 32800:80

* Create the container 
----------------------
    ^ docker container run -d --name trail -P spc:1.0.2
    ^ 

## <command> <arguments>
* arguments are identified by spaces
    Ex:-
        cp 1.txt 2.txt
    cp = command
    1.txt 2.txt = arguments

## Arguments:
    1. Named arguments (Keyword)
    2. Positional arguments
    
----------------------------------------------------------------------------
## 26/08/23 - [Terraform workshop]
------------
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
### Containerization using Dockerfile
-------------------------------------
Web:- Docker file reference.

* Use alias -------RT (08:45)
    ^ vi ~/.bashrc (ec2 instance)
inside vi add this files
  - alias rmi='docker image rm -f `docker image ls -q`'
  - alias rmc='docker container rm -f `docker container ls -a -q`'
    ^ source ~/.bashrc
    ^ rmc 
now rmove all the containers
----
# Building spc
--------------
* [Dont run your container in root user]
ADD your ubuntu user into the docker group
    ^ sudo usermod -aG docker ubuntu
do work now
---

    ^ adduser --help        ---------> RT(27:04)
    ^ adduser -h /petclinic -s /bin/sh -D petclinic
-D (passwd)

image build - arguments 
application build - environment varaible

# Environmet varaible (ENV)  ----RT(01:35:00)
---------------------------
    - every os hans an ENV

* how to know what is your environmet varaibels...?
    ^ printenv
eg:- USER=ubuntu <enviromentvaraibel=valu>

    ^ docker container run -P --name pc1 -d petclinc:vi.0.0-slim
    ^ docker container exec pc1 printenv    
---evnironmental variables---

```bash ----RT(59:00)
FROM amazoncorretto:11-alpine3.17
LABEL author="Runner"
LABEL organization="gamezoneworld"
ARG DOWNLOAD_LOCATION="https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar"
ARG HOME_DIR=/spc
ARG uid=1001
ARG user=spring
ARG group=spring
# ENV TEST=hello  ---------RT(01:39:00)
RUN adduser -h ${HOME_DIR} -s /bin/sh -D -u ${uid} ${user}
USER ${user}
WORKDIR ${HOME_DIR}
ADD --chown=${user}:${group} ${DOWNLOAD_LOCATION} ${HOME_DIR}/spring-petclinic-2.4.2.jar
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic-2.4.2.jar"]
```
==========================================================================
## 29/08/23
-----------
Exercise Solution 
* Game of Life 
    Requirments -tomcat:9 and jdk8
    DockerHub search `tomcat:9-jdk8`
Create an EC2 (ubuntu-t2.micro)
    ^ docker container run -d -P --name <..> tomcat:9-jdk8
    ^ docker container exec -it <...> /bin/bash
    ^ ls (webaps)
    ^ cd webaps
    ^ wget https://khaja sir refrer......
[https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war]
    ^ docker container ls -a
copy the port ID and open in web page 

# Exercise
* Run the aws s3 files in same game of life application    
--xx--

### Single Stage Dockerfile (NopCommerce)
* Nop Commerce (singel stage) ---RT(50:00)
 Create an EC2 (ubuntu-t2.micro)
    clone the nopCommerce url `https://github.com/nopSolutions/nopCommerce`
    
vi Dockerfile
```


FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL author="tiru" organization="qt"
WORKDIR /Ram
COPY /nopCommerce_4.60.4_NoSource_linux_x64.zip /Ram
RUN apt update && apt install unzip -y && \
    mkdir /Ram/bin && mkdir /Ram/logs && \
    unzip /Ram/nopCommerce_4.60.4_NoSource_linux_x64.zip
EXPOSE 5000
CMD ["dotnet","Nop.Web.dll","--urls","http://0.0.0.0:5000"]
```
1. FROM (docker hub --> search .NET --> Featured Repos {dotnet/sdk: .NET SDK} --> Featured Tags {mcr.microsoft.com/dotnet/sdk:7.0})

4. COPY (after unzip {nopcommercegithub --> releases --> nopCommerce_4.60.4_NoSource_linux_x64.zip (copy the zip file - APC ^ wget <zipfile>)} the nopCommerce file we have and git file name </Ram>)

5. RUN apt update && install && mkdir bin logs && unzip 
   
======================================================================
## 31/08/23 [Mrng]
------------------
### Multi stage Dockerfile (SPC) ----RT(26)
-------------------------------------------
    [JDK17 and MAVEN]

    - Use springpetclinic github and git clone that https code
[https://github.com/spring-projects/spring-petclinic]
    ^ git clone https://github.com/spring-projects/spring-petclinic

    - "mvn package" - docker.hub and find maven, in this maven jdk versions are avilable.
[https://hub.docker.com/_/maven] - maven:3-amazoncorretto-17
        - if you know the maven version work or not - After git clone and run the container and check the version of maven   
    ^ docker container run -it maven:3-amazoncorretto-17
        check the maven version 
            ^ mvn --version 
        maven is prestnt

========>
`in reality`
<!--  
    ^ git clone https://github.com/spring-projects/spring-petclinic
    ^ cd /spring-petclinic
  in that /spring-petclinic write an 
    `vi Dockerfile` -->
IN VSC---->
* `DOCKER-IGNORE`
[NOTE:- if you dont want sutten things in Dockerfile - create one more `.dockerignore` file ]
    - inside the .dockerignore file add `*.txt, *.md `

* `DOCKERFILE`
    - add singel step dockerfile

* `DOCKERFILE.MULTI`
    - In this file add contents of your file `FROM, COPY, RUN ......`

```bash
FROM maven:3-amazoncorretto-17
COPY . /spring-prtclinic
RUN cd /spring-prtclinic && mvn package
```
    ^ docker image build -t spc:1.1 .
    ^ docker contaner run -d -P --name jai spc:1.1
how can we know package of image 
    ^ docker container run -it spc:1.1 /bin/bash
    ^ cd spring-petclinc/
    ^ ls ---> target folder
    ^ cd target/
    ^ ls ---> spring-prtclinic-3.1.0-ANAPCHOT.jar
  -exit-
now write a Dockerfile
```bash
FROM maven:3-amazoncorretto-17 AS builder
COPY . /spring-petclinic
RUN  cd /spring-petclinic && mvn package

FROM amazoncorretto:17-alpine3.17
LABEL author="khaja"
LABEL organization="learningthoughts"
ARG USERNAME='petclinic'
ARG HOMEDIR='/petclinic'
ENV TEST=hello
RUN adduser -h ${HOMEDIR} -s /bin/sh -D ${USERNAME}
USER ${USERNAME}
WORKDIR ${HOMEDIR}
COPY --from=builder --chown=${USERNAME}:${USERNAME} /spring-petclinic/target/spring-petclinic-3.1.0-SNAPSHOT.jar "${HOMEDIR}/spring-petclinic-3.1.0-SNAPSHOT.jar"
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic-3.1.0-SNAPSHOT.jar"]
```
=======>

* Clone spc-repo   
* add Dockerfile with following contents and build image 
[vi Dockerfile]
```bash
FROM maven:3-amazoncorretto-17
LABEL 
COPY
```
    ^ docker image build -t spc:multi .
    ^ docker container run -it -P spc:multi /bin/sh
    ^ pwd
    java -jar spring-petclinc 
    

=========================================================================

## 01/09/23
-----------
How to Puah the image 
    in dockerhub, jfrog, eks, aks
=========================================================================
## 02/09/23 [Mrng]
------------------
### Networking in Containers
-----------------------------
* Layers in Docker Image:
-------------------------
* Docker Networking Series – I
    - Docker Networking is Linux Networking
[https://directdevops.blog/2019/10/05/docker-networking-series-i/]

* Docker Playground
    pull the image - alpine:3.17
    ^ docker image pull alpine:3.17
    ^ docker image inspect alpine:3.17 - information about alpine

    ^ docker image pull jenkins/jenkins
    ^ docker image inspect jenkins/jenkins
    ^ mkdir test - cd test
    ^ vi Dockerfile

```bash
FROM alpine:3.17
```
    ^ docekr image build -t exp:1.0 .
    ^ docker image inspect exp:1.0
    ^ dokcer image ls
REPOSITORY        TAG       IMAGE ID       CREATED       SIZE
 jenkins/jenkins   latest    c9101035cede   6 days ago    478MB
`exp               1.0       f30308d6110e   6 weeks ago   7.06MB`
 alpine            3.17      1e0b8b5322fc   6 weeks ago   7.06MB

    ^ vi Dockerfile
```bash
FROM alpine:3.17
ADD https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war /gameoflife.war
```
    ^ docker image build -t exp:1.1 .
    ^ docker image ls
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE `exp               1.1       804167b3c04e   19 seconds ago   10.3MB`
 jenkins/jenkins   latest    c9101035cede   6 days ago       478MB
 alpine            3.17      1e0b8b5322fc   6 weeks ago      7.06MB
 exp               1.0       f30308d6110e   6 weeks ago      7.06MB


    ^ docker image inspect exp:1.1
"Layers": [
    "sha256:36b50b131297b8860da51b2d2b24bb4c08dfbdf2789b08e3cc0f187c98637a19",
    "sha256:d318847c9d68fcbd5f80f6800caea12b97a6cdc3a500c7b64f2f8283899c9f0e"
            ]
    
    ^ vi Dockerfile
```bash
FROM alpine:3.17
ADD https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war /gameoflife.war
RUN mkdir test
RUN cd /gameoflife.war /test/gameoflife.war
```
    ^ docker image build -t exp:1.1 .
    ^ docker image ls
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
`exp               1.2       579d8fc63731   6 seconds ago    13.4MB`
 exp               1.1       804167b3c04e   27 minutes ago   10.3MB
 jenkins/jenkins   latest    c9101035cede   6 days ago       478MB
 exp               1.0       f30308d6110e   6 weeks ago      7.06MB
 alpine            3.17      1e0b8b5322fc   6 weeks ago      7.06MB


    ^ docker image inspect exp:1.2
"Layers": [
    "sha256:36b50b131297b8860da51b2d2b24bb4c08dfbdf2789b08e3cc0f187c98637a19",
    "sha256:d318847c9d68fcbd5f80f6800caea12b97a6cdc3a500c7b64f2f8283899c9f0e",
    "sha256:576e525ec234e1414336a26871ac0c9e18f066252735726cd1ab6b07ba5c3981",
    "sha256:a60cf463dbc9619877c08ea729be78ee3f355053f143fca5fafd3cfcedffa623"
            ]
refer to
[https://directdevops.blog/2019/09/27/impact-of-image-layers-on-docker-containers-storage-drivers/]

    ^ vi Dockerfile
```bash
FROM alpine:3.17
ADD https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war /gameoflife.war
RUN mkdir test && \
    cp /gameoflife.war && \
    /test/gameoflife.war && \
    java -version > version.txt
```

## ENTRYPOINT and CMD in docker files
-------------------------------------
    - Command which gets executed when the docker container is created from image.
    - CMD acts as argument to the ENTRYPOINT
refer to docker file 
    [https://directdevops.blog/2019/09/26/docker-image-creation-and-docker-image-layers/]

----
* Fork:
    - Fork is a system call that creates a new process (child process) by duplicating the existing process (parent process)

* Exec:
    - Exec is a family of system calls (e.g., execv, execl, execve, etc.) 
    - used to replace the current process's memory image with a new program. 
`---xx---`
* Shell form:
    - The command as a single string, which is interpreted by a shell (typically /bin/sh) within the container.
    - Commands are written without [] brackets and are run by the container's shell, such as /bin/sh -c

* Exec Form:
    - The command as an array of strings, where the first string is the command to be executed, and the subsequent strings are arguments passed to that command. 
    - Commands are written with [] brackets and are run directly, not through a shell.
`---xx---`
Bulding an Image (SPC)
    - Manually to execute spring pet clinic
[https://directdevops.blog/2019/09/26/docker-image-creation-and-docker-image-layers/]

### Docker volumes: ----RT(01:47:00)
    - Docker volumes are a way to manage and persist data in Docker containers
[https://directdevops.blog/2019/10/03/docker-volumes/]

* Docker Image Creation and Docker Image Layers:
    [https://directdevops.blog/2019/09/26/docker-image-creation-and-docker-image-layers/]

* Impact of Image Layers on Docker Containers & Storage Drivers:
    [https://directdevops.blog/2019/09/27/impact-of-image-layers-on-docker-containers-storage-drivers/]


* Port forwarding (-p / --publish)
-----------------
  - the process of mapping ports on the host system to ports on a Docker container, allowing external applications to access services running inside the container.
  -  

* Docker Compose:
-----------------
  - Docker Compose is a tool for defining and running multi-container Docker applications.
  - `docker-compose.yml`
  - This YAML file specifies services, networks, volumes, and other settings for your containers.
![refer](image-2.png)

* Dynamic Port Allocation:
--------------------------
  - Docker allows you to automatically assign a free port on the host system to a container's exposed port without specifying a port number explicitly.
  - `-P or --publish-all`


# Docker volumes
----------------
    - Docker, a volume is a managed directory or data storage mechanism that exists outside of the container's file system but can be mounted into one or more containers.

Three types 
  1. Bind Mounts
    - some exceisting folder in your docker host to some folder in docker container.
    - to make files and directories on the host system available inside containers.
    `-v or --volume`
 Eg:- docker run -v ~/host/path:/container/path my_image
    `~/host/path` is the path on the host machine where the directory or file exists.
    `/container/path` is the path inside the container where the bind mount will be mounted.

  2. Volumes Mounts
    - to make files and directories on the host system available inside containers.
    - Docker volume mounts are a way to manage and persist data by mounting volumes into containers.
    `-v or --volume` 
 Eg:- docker run -v my_volume:/container/path my_image
    `my_volume` is the name of the Docker volume you created in step 1.
    `/container/path` is the path inside the container where the volume will be mounted.

  3. tmpfs Mounts
    - in tempfs mounts is some part of mount is stord in ram on the host system, onece shut down the host we louse the ram....
    - Docker, a tmpfs mount is a special type of mount that allows you to create an in-memory file system that exists only in a container's memory
    `--tmpfs`
 Eg:- docker run --tmpfs /path/in/container:options my_image
    `/path/in/container` is the path inside the container where the tmpfs mount will be created.
    `options` are optional, and you can specify additional mount options like size limits
   
* Create Docker Volume:-    ---------RT (01:50:00)
    ^ docker volume --help
    ^ docker volume create docs-vol
    ^ docker container run -d --name test -v docs-vol:/docs alpine sleep 1d
    ^ docker container exec -it test /bin/sh
<!--^ touch /docs/{1..10}.txt  (this command work in /bin/bash only)
<!-- command not found because /bin/sh are not create {write scripte vise like touch 1.txt 2.txt .....} -->
    ^ touch 1.txt 2.txt
exit
    ^ docker container rm -f test
    ^ docker volume ls (docs-vol)

    ^ docker volume inspect docs-vol
    ^ ls /var/lib/docker/volumers/docs-vol/_data
1.txt 2.txt
    ^ ls -al /var/lib/docker/volumers/docs-vol/_data

---xx---

# Docker volume drivers:- -------RT (01:50:00)
-------------------------
    - Docker volume driver can be specified while creating a volume or when to start the container.

Create mysql database
 DockerHub - mysql (start a mysql sever instance command) 
    ^ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
    ^ docker container ls {mysql is running}
    ^ docker volume ls {strange volume is comming}

{`VOLUME` - Docker, a volume is a directory or data storage mechanism that exists outside of the container's file system but can be mounted into a container.
`VOLUME PATH`:- /var/lib/mysql }

* Now create a volume and mount it it mysql with same `specific-mysql` ---RT (02:04:30)
    ^ docker volume create nop-vol
    ^ docker run --name specific-mysql -v nop-vol:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -P -d mysql
    ^ docker volume ls
    ^ docker volume inspect nop-vol  {mountpoint: "/var/lib........"}
 create some data inside a database:- 
    ^ docker container exec -it specific-mysql mysql -uroot -p
 Enter password: my-secret-pw
  inside mysql
    ^ show databases;
    ^ create database nop;
    ^ show databases;
 exit
 delete container 
    ^ docker container rm -f specific-mysql
 create new container and same volume:-
    ^ docker run --name reborn-mysql -v nop-vol:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -P -d mysql
    ^ docker container exec -it reborn-mysql mysql -uroot -p
Enter password: my-secret-pw
  inside mysql
    ^ show databases;
 nop is present....

--xx--New vm
* Now create the container `some-mysql` and look at volumes ---RT (02:11:00)

    ^ mkdir nop && cd nop
    ^ vi Dockerfile {nopcommace - alpine:3 as downlader}
```
nopCommerce file
```
    ^ docker image build -t nop .
    ^ docker image ls
    ^ docker image pull mysql:8
    ^ docker volume create nop-db
    ^ docker container run -d --name nopdb -e MYSQL_ROOT_PASSWORD=nop123 -e MYSQL_DATABASE=nop -e MYSQL_USER=nop -e MYSQL_PASSWORD=nop123 -P -v nop-db:/var/lib/mysql mysql:8
    ^ docker container ls
    ^ docker image ls
    ^ docker container run -d --name nop -P nop:latest
    ^ docker container ls
check your port....
 
 install NopCommerce application ---RT (02:24:00)
   if any information about application.......
    ^ docker container inspect nopdb (server name of nop)

    incase container is stop
        ^ docker container start nop
        ^ docker container ls
    port no.....

Total database is storge in `nop-db`
    ^ docker volume ls
    ^ docker volume inspect nop-db

    ^ cd /var/lib/docker/volume/nop-db/_data
    ^ ls
    ^ cd nop
all the mysql database are present....

=> what is volume use for...?
=> what is the multiple layer 
=> how to communicate two different pods in containers --- volumes 

=> monolith component (Eg: docker engine)
=> lib container and lib network
=> main car containers vs side car 

## 02/09/23 [Even]
------------------
### Networking in Containers
-----------------------------
[https://directdevops.blog/2019/10/05/docker-networking-series-i/]

Docker - Container Networking Model (CNM)
K8s - Container Networking Interphase (CNI)

* Container Networking Model (CNM)
    - Docker interact with networking plugins to provide network connectivity to containers. 
    - Docker defined a standard for container networking called as Container Networking Model (CNM)

=> Nerwork IP - The first part of an IP address
=> Host IP - the last part as a host address
=> Subnet mask - a logical subdivision of an IP network.
        subnet has 32 bit number    
        this 32 bit number dived into 16+16
            firsr 16= network id
            second 16= host id
    
* Range of IP (Internet Protocol) addresses availabel 
IP addresses is a 32 bit number 
    these 32 bit(possion) are broke into 4 equal parts (32/4=8)
     Eg:- X.X.X.X  (four decimal numbers separated)=> IPv4
        in IPv4 --> 192.168.0.1
    in each bit number is 0 or 1

  IP addresses range 0.0.0.0 to 255.255.255.255 -
                     192.168.0.0 to 192.168.255.255 (private network)

* Private Network CIDR ranges:-
[https://www.google.com/search?q=private+cidr+ranges&rlz=1C1CHBD_enIN989IN989&oq=private+cidr+ranges&aqs=chrome..69i57j0i22i30l4j0i390i650l2.9785j0j7&sourceid=chrome&ie=UTF-8]

=> IP addresses 
=> CIDR (Classless Inter-Domain Routing)
    - CIDR allows for more flexible allocation of IP addresses
    - Used in IP (Internet Protocol) addressing and routing to allocate and manage IP addresses more efficiently.

* CIDR Expander
[https://www.ipaddressguide.com/cidr]

* DHCP (Dynamic Host Configuration Protocol)
    - a protocol for automatically assigning IP addresses and other configurations to devices when they connect to a network. 

* ifconfig (interface config)
    - displays the current configuration for a network interface when no optional parameters are supplied.

* install Docker using ubuntu vm
    ^ sudo apt update && sudo apt install net-tools -y
    ^ ifconfig
        - 2 interfaces are hear 1.eth0 and 2. lo (loopback)
        - check your eth0 ip addresses to CIDR Expander
  Docker installation script
    ^ sudo usermod -aG docker ubuntu 
  Exit & relogin
    ^ ifconfig
        - new network inderfase (docker interfase) are created
        - 3 interfaces are hear `dokcer0, eth0, lo (loopback)`
    ^ docker nerwork ls
    ^ docker network inspect ls

* Brige network     -----RT (34:00)
---------------
    - Brige Networking is a divise that conntected two networks as if they are together.
 Brige = Docker0 IP --->connected to---> container IP

* Port forwarding (port mapping)
--------------------------------
    - forward network traffic from one port on a router or firewall to another port on a different device within a local area network (LAN).

* LAN (local area network)

--xx--
* Create a new network in Docker
    ^ docker network create --subner "192.168.0.0/24" testnet
    ^ docker network ls
    ^ ifconfig
  now testnet network created...
   
 ^ docker container inspet

**** Create a own network and run the container whith in the network

---------------------------------------------------------------------------  
# Docker Networking Architecture
---------------------------------
[https://directdevops.blog/2019/10/05/docker-networking-series-i/]

* Lib Network:-
    - Libnetwork was responsible for creating and managing networks within the Docker ecosystem.

# Docker Native Network Drivers
[https://directdevops.blog/2019/10/05/docker-networking-series-i/]
* Host:
    - Container uses the networking stack of the host.
* Brige:
    - Brige is never use for multi nod, it's works in one machine

* Overly:
    - Used for multi-host networks.
    - Overly is never use for single nod, it's works acrose machine

* Macvlan:
    - one types of brige network

*  None:
    - Container willbe created with no network
    - 
# Docker Networking Scopes
[https://directdevops.blog/2019/10/05/docker-networking-series-i/]

* DNS (Domain Name System):-
    - a protocol used in computer networking and the internet.
   - Domain Names: (e.g., www.example.com)

# Experiment: Interaction between two containers in default bridge

    ^ docker container run --name C1 -d alpine sleep 1d
    ^ docker container run --name C2 -d alpine sleep 1d
* IP addresses of docker bridge
    ^ docker network inspect bridge

* Now lets ping C2 from C1 by using ip as well as name
    ^ docker container exec C1 ping -c 4 <C2 IP adderess>

   
# Create nop-commerce application by creating volumes and networks --RT(01:30:00)
* single node
    ^ mkdir nop & cd nop
    ^ vi Dockerfile
```
<nop file> [https://github.com/runtiru/Docker/blob/main/NopCommerce/multi%20stage/Dockerfile]
``` 
    ^ docker image build -t nop .
* Steps
  - create a volume <nop-db>
    ^ docker volume create nop-db
  - create a network <nopnet>
    ^ docker network create -d bridge --subnet '10.100.100.0/24' nopnet

* Create a mysql container 
  - username nop, volume, password `nop123` in nopnet with name `nopdb`
  - Environmetal variables
```bash
docker container run -d --name nopdb \
    --network nopnet \
    -e "MYSQL_ROOT_PASSWORD=nop123" \
    -e "MYSQL_USER=nop" \
    -e "MYSQL_PASSWORD=nop123" \
    -e "MYSQL_DATABASE=nop" \
    -v nop-db:/var/lib/mysql \
    mysql:8
```
* Create the nop container on nopnet
    ^ docker container run -d --name nop --network nopnet -P nop
    ^ docker container ls 
<!-- f79abb16e307   nop       "dotnet Nop.Web.dll"     10 seconds ago   Up 9 seconds    0.0.0.0:32768->5000/tcp   nop
4fead742e364   mysql:8   "docker-entrypoint.s…"   39 seconds ago   Up 39 seconds   3306/tcp, 33060/tcp       nopdb -->
    ^ docker network inspect nopnet
        "Containers": {
            "4fead742e364200ed4477c29b2b267f26b5b185a1f33bb5d21ed1ac9c94f5aa9": {
                "Name": "nopdb",
                "EndpointID": "23104e2250b7c751f1abe54bb174043482b9088ef94d8a36dfd5eb08ad2d5a0f",
                "MacAddress": "02:42:0a:64:64:02",
                "IPv4Address": "10.100.100.2/24",
                "IPv6Address": ""
            },
            "f79abb16e307a876f09f21390a12521b9f80c7a7f12cd7f84b7090ae983deece": {
                "Name": "nop",
                "EndpointID": "f3573611fc1ca4b42f98baac52a24d18b0f451b4588f401f0388ed68942a2c3d",
                "MacAddress": "02:42:0a:64:64:03",
                "IPv4Address": "10.100.100.3/24",
                "IPv6Address": ""
            }}
    ^ docker container ls 
        - now login to nopCommerce application, useing to nopdb IP <32768>

====================================================================================

## 03/09/23 [Mrng]
------------------
### Networking in Containers
-----------------------------
* Create an EC2 with docker 
    ADD the USER DATA in instance file 
```bash
#!/bin/bash
cd /tmp && curl -fsSL https://get.docker.com -o install-docker.sh && sh install-docker.sh && usermod -aG docker ubuntu
```
    ^ docker version
if the docker version not installed use the command 
            ^ cat /var/log/cloud-init-output.log
now docker installed  check the version of docker
    ^ exet & relogin
    ^ docker info (get the docker full information)
--xx--

### YAML
```yaml
---
name: Mani's Resturent
wifi: yes
table: 10
chairs: 30
owners:
  - mani
  - raj
  - manu
menu:
  - name: coffee
    price: 50
  - name: tea
    price: 30
  - name: chai
    price: 30
```

### JSON
```json
{
  "name": "Mani's Resturent",
  "wifi": "yes",
  "table": 10,
  "chairs": 30,
  "owners": [
    "mani",
    "raj",
    "manu"
  ],
  "menu": [
    {
      "name": "coffee",
      "price": 50
    },
    {
      "name": "tea",
      "price": 30
    },
    {
      "name": "chai",
      "price": 30
    }
  ]
}
```
## Docker Compose
-----------------
    - Defining and Running multi-container Docker applications. 
    - With Compose, you use a YAML file to configure your application's services.
    - Create and start all the services from your configuration.
    - It's used only developer invironmet.
[https://docs.docker.com/compose/compose-file/03-compose-file/]

# Write a docker compose for spring petclinic:-
    - create a Dockerfile and build the image (spc/nop)
    




