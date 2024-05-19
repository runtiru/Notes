------------------------------
# 19/07/23...
------------------------------
### How to add multipule nodes to jenkins
    --------------------------------------
            Spc project --> JAVA-17 - node-1
            Game of life --> JAVA-8 + maven - node-2
            Nopcommerce --> DOTNET-7 - node-3

* Create 3 virtual machine - ec2 ubuntu instance (mediam)
            1- jenkins_master
            2- node-1
            3- node-2

1- Jenkins_master         2- node-1                 3-node-2
    install java-17            install java-17          java-8
    jenkins                    maven-3.9                maven-3.9

1. Jenkins_master
    ^ sudo apt update
    ^ sudo apt install openjdk-17-jdk -y
    ^ vi installjenkins.sh   (nots qtdevops-19th class)
```bash
#!/bin/bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```
(:wq!)
    ^ chmod +x installjenkins.sh
    ^ ./installjenkins.sh
    ^ sudo visudo 
        give a permision (jenkins ALL=(ALL:ALL) NOPASSWD:ALL)
    ^ sudo -i
    ^ su jenkins
    ^ cd ~
    ^ sudo apt update
          once done apt update-( jenkins@ip-172-31-90-89:~$ )
                                 
-----------
Goto Ec2 instance and copy the jenkins_master public ID
    new tap on windous 
        (past public ID:8080)
    now some var file ie (/var/lib/jenkins/secrets/initialAdminPassword)
            paste the var file with ( SUDO CAT )in APS and get the password (822e62969d18491fa1f0059a29f7a028) copy 
            apst the new windows
    start JENKINS
            Create First Admin User (what ever it)
    Instance Configuration
            (save and finish)
            ----------------
2. node-1
---------
    ^ ssh ubuntu@ID
    ^ sudo apt update && sudo apt install openjdk-17-jdk -y
    ^ cd /tmp/            ----> (nots qtdevops-16th class)
    ^ wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
    ^ sudo mkdir /usr/share/maven
    ^ sudo tar -xvzf apache-maven-3.9.3-bin.tar.gz -C /usr/share/maven

             (((     ^ cd /usr/share/maven/
                     ^ ls
                     ^ cd apache-maven-3.9.3
                     ^ ls
                     ^ cd /bin/
                     ^ pwd  )))
        Copy the command - /usr/share/maven/apache-maven-3.9.3/bin
    ^ ::: exit untill /tmp/
    ^ sudo vi /etc/environment      --------- (# ~/.bashrc or /etc/envionment)  
### (/usr/share/maven/apache-maven-3.9.3/bin)
(:wq!)
    ^ exit 
    (and relogin-PgDn key) 
    ^ mvn --version
            Apache Maven 3.9.3
            Maven home: /usr/share/maven/apache-maven-3.9.3
            Java version: 17.0.7
-------------
### configure node to the jenkins master with label 'JDK-17'
        open jenkins
Manage jenkins
    Nodes and Clouds
       Create a node
        Name - node-1
        TYPE - Permanent agent
--CREATE--
------------
    DESCRIPTION - This is my node with openjdk 17 and maven 3.9
    NUMBER OF EXECUTORS - 2
    REMOTE ROOT DIRECTOEY - /home/ubuntu/jenkins_root/
    LABELS - JDK-17 (red)
    USAGE - only jobs with lable expression matching this node
---------
    LAUNCH METHOD - launch agents via SSH
        HOST - (Private IP of NODE-1 )
        CREDENTIALS -  
    ADD ^jenkins^
            DOMAIN - Global credentials
            KIND - SSH Username eith 
            
            private key
                SCOPE - Global(jenkins,nodes,item,all child items.etc)
                ID - UBUNTU_ID_RSA                    
                DESCRIPTION - this is my key for ubuntu
            USERNAME - Ubuntu
            PRIVATE KEY - 
                (OK) Enter directly
                    key - PRIVATE KEY           
            (Add)
    {{Coming to APS:- ^ notepad C:\Users\BALU\.ssh\id_rsa
                (copy the key)}}
                    Add key
    CREDENTIALS - (this is my key for ubuntu)
    HOST KEY VERIFICATION - Non verfying verificaion strategy
            SAVE
--------------
### Lets setup spring petclinic to execute node-1
Create new fork IP on Spring-petclinic (copy https IP)
        goto fork (+ create new)
   -----
   Create an + New Item (on jenkins)
        Name - spc-day-build
            free style project
    --OK--
GENERAL - 
    RESTRICT WHERE THIS PROJECT CAN BE RUN
        LABEL EXPRESSION - JDK-17
SOURCE CODE MANAGEMENT -
    GIT - 
        REOP URL - (Past the SPC - IP)
        CREDENTIALS - none
     BRANCH SPECIFIER - (*/main)
BUILD TRIGGERS - 
    POLL SCM - * * * * *
BUILD STEPS - 
    INCOKE TOP-LEVEL MACEN TARGETS - 
        GOLS - package
    SAVE
---------
BUILD NOW
---------
EVEN ERROR IS COMMING 
    open node-1 (APS)
        ^ ls
        ^ cd jenkins_root/
        ^ ls
            (remoting remoting.jar workspace)
        ^ cd workspace
        ^ ls
            (spc-day-build)
        ^ cd spc-day-build
        ^ ls
            (licence.txt build.gradle mvn mvnw.cmd pom.xml )
        ^ ip addr

------------------------------
# 20/07/23... GAME OF LIFE 
------------------------------
### Node-2 => JDK 8 and maven
    'game of life' we would require 'jdk8'
        create one ec2 ubuntu instant (node-2)
    On the node2 create a new user called as "devops"    

* now login to node-2 in APS:-
    ^ ssh ubuntu@ID
    ^ sudo adduser devops
        new passwd.........
        .....
    ^ sudo visudo 
        (give sudo no password access - devops ALL=(ALL:ALL) NOPASSWD:ALL)
        (enable password based authentication)
    ^ sudo vi /etc/ssh/sshd_config
        (PasswordAuthentication 'yes')
     (:wq!)
    ^ sudo systemctl restart sshd
    ^ exit and relogin (PgDN)
    ^ ssh devops@ID
    Passwd set (aa) ---> (devops@ip-172-31-84-146:~$)
### Install jdk 8 and jdk 17
    ^ sudo apt update
    ^ sudo apt install openjdk-8-jdk openjdk-17-jdk -y
    ^ sudo apt install maven -y
    ^ java -version
                openjdk version "17.0.7" 
                OpenJDK Runtime Environment 
                OpenJDK 64-Bit 
    ^ whereis java
        (java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1.gz)

    ^ ls -al /user/share/java/
        (/etc/alternatives/java)

    ^ ls -al /etc/alternatives/java
        (/usr/lib/jvm/java-17-openjdk-amd64/bin/java)

    ^ cd /usr/lib/jvm/
    ^ ls
        (all versions of JAVA like -- java-1.17.0-openjdk-amd64  java-17-openjdk-amd64  openjdk-17
java-1.8.0-openjdk-amd64   java-8-openjdk-amd64 )

    ^ cd java-17-openjdk-amd64/
    This is the path - (/usr/lib/jvm/java-17-openjdk-amd64)
------------------
### Configure JDK 17 and JDK 8 paths in tools section of jenkins ---> RT (12:00) 
        (open jenkins master_node )
Manage Jenkins
    TOOLS - 
        JDK installation
    ADD JDK -
        NAME - JDK_17
        JAVA HOME - /usr/lib/jvm/java-17-openjdk-amd64 (open node-2 in APS ^ ls (list of JDK-17 version))
      (note never install automatically)
    ADD JDK -
        NAME - JAVA_8
        JAVA HOME - /usr/lib/jvm/java-8-openjdk-amd64   (open node-2 in APS ^ cd ../java-8-openjdk-amd64/ (list of JDK-8 version))
      (note never install automatically)
 --SAVE--

### "Now lets try building game of life"
    open web "game of life" -
        Create a fork - (copy the https ID)
Create + New Item
        name - gameoflife (free style project)
Source code management
    GIT -
        Reopsitory URL - (past the game of life ID )
    Credentials - no need -
    Branches to build - 
        */master
Build Enviranment - 
    Build steps - 
        Add build step^
            invoke top-level maven targets
                Goals - package
                    Advanced^
                    check - JVM Options
--------------------------
MANAGE JENKINS
    TOOLS - 
        MAVEN INSTALLATIONS
            Add Maven
                NAME - MAVEN_DEFAULT (open node-2 in APS " ^ whereis maven")
                                    (maven: /etc/maven/usr/share/maven)
                MAVEN_HOME - (/usr/share/maven)
---------------------------
    open node-1 in APS
        ^ ssh ubuntu@ID
        ^ cd /usr/share/maven
        ^ ls (apache-maven-3.9.3)   
        ^ cd apache-maven-3.9.3 
        (/usr/share/maven/apache-maven-3.9.3)
                (this is the path of maven 3.9)
--------------------------
            Add Maven   
                NAME - MAVEN_3.9
                MAVEN_HOME - (/usr/share/maven/apache-maven-3.9.3)
    save...
------------
------------
In spc-day-build project
    configure
        Build steps
            Invoke top-level Maven targets
                Maven version - (MAVAN_3.9)
                Goals - (package)
    SAVE and BUILD NOW ---- (RT:18.00)
        -----------------
### Now add node2 to jenkins
    + New Node
        Node Name - node2
        Permanent Agent
--Create--
    Description -
    Number of ececutors - 1
    Remote root directory - /home/devops/jenkins_root
    Labels - JDK_8
    Usage - only build jobs eith experssions ......
    Launch method - launch agent via SSH
        HOST - (Private IP of NODE-2 )
        CREDENTIALS -  ADD ^jenkins^
            DOMAIN - Global credentials
            KIND - Username with password
                SCOPE - Global(jenkins,nodes,item,all child items.etc)
                Userneme - devops
                Password - "aa"
                ID - DEVOPS_USER
                DESCRIPTION - this is service account
--(ADD)--
        CREDENTIALS - devops/*****(this is service account)

        HOST KEY VERFICATION STRATEGY - Non verfying verfication strategy
    Node Properties
        tool location
            list of tool locations
                Name - JDK_17
                Home - /usr/lib/jvm/java-17-openjdk-amd64
            (Add)
                Name - MAVEN_3.9
                Home - /usr/share/maven/apache-maven-3.9.3
    ---(SAVE)---
     Open node-2 (on jenkins)
        LOG -- "succusfull"
#
# (((NOTE :we are already done this one - goto 213 no ))) 
# 
### "Project - game of life"
    Configure
        BUILD STEPS
            (ADD B.S)
    INVOKE TOP-LEVEL MAVEN TARGETS
        Maven version -(Maven_default)
        Goals (package)
            Addvance options -
                check errors/failurs (user default)

    (open web "game of life" -
        already created fork - (copy the https ID))
    
Source code management
    GIT -
        Reopsitory URL - (past the game of life ID )
    Credentials - no need -
    Branches to build - 
        */master
        
General - 
        JDK -
            JDK to be used project - (JAVA_8)
    Select Restrict where this project can be run
            Label Expression - (JDK_8)
    --(SAVE)--
--(BUILD NOW)-- SUCCESS         -----> (25:00)
# add processing the test results **/surefire-reports/TEST-*.xml
    goto game of life - configure
        Build triggers
            Poll SCM - (* * * * * - ever minute )
        Build steps -
            Invoke top-level Maven targets
                (add build steps)
        Post-Build Actions
            Publish JUnit test reports
            text reports - XMLs - **/surefire-reports/TEST-*.xml

                                    ((goto node-2 APS
                                     ^ cd ~
                                     ^ ls
                                     ^ cd jenkins_root/
                                     ^ cd workspace/gameoflife/
                                     ^ cd gameoflife-web/ 
                                     ^ ls
                                     ^ cd target/
                                     ^ ls 
                                     ^ ls surefire-reports/ ))
            --(SAVE)--
        ---Build Now---
## Artifact
        ## lets configure jenkins to archive the artifacts
Configure (gameoflife) 
   Post-build Actions
    (Add a post build actions)
        Archive the artifacts
            file to archive - **/gameoflife.war (or) gameoflife-web/target/gameoflife.war
--(SAVE)--
----(BUILD NOW)---- SUCCESS
    Refress - some war file are coming (gameoflife.war)
-----------------------------------
### same artifact add in (spc-day-build)
Configure (spc-day-build) 
   Post-build Actions
    (Add a post build actions)
        Archive the artifacts
            file to archive - **/target/spring-petclinic-*.jar
    (Add onemore pos build actions)
        Publish JUnit test restlt report
            text reports - XMLs - **/surefire-reports/TEST-*.xml
--(SAVE)--
----(BUILD NOW)---- SUCCESS    
    Refress - some war file are coming (spc-day-build.war)    
------------------------------------
------------------------------------
### Executing dotnet project on jenkins ------> RT(37:00)
##   Node-3:
        * For agent we required jdk 17
        * Create an ec2 instance with size 20 GB
        * install dotnet 7 sdk for running nop comerce
    
Create virtual machine - ec2 ubuntu instance (20.04 + mediam - 15GB)
        Name - node-3
            connect your linux - node-3
      
    goto web - "installing dotnet 7 in on ubuntu 20.04"
    (Note DONT COPY HEAR - VSC)
    ^ sudo apt-get update && sudo apt-get install -y dotnet-sdk-7.0

Now install jave in node -3
    ^ sudo apt install openjdk-17-jdk -y

## Build the dotnet project we need to restore nuget packages -----> RT(42:00)

    # dotnet restore <path of project or sln>
goto nopcommerce github.com
    copy the nopcommers github https - IP
    ^ cd /tmp/
    ^ git clone (nopcommers github https - IP)
-----
    configure 3rd node of jenkins ------> RT(48:00)
        Manage Jenkins
            Node 
                + New node
        Name - node-3
        Permanent Agent
--(Create)--
        Numbers of executors - 2
        Pemote root directory - /home/ubuntu/jenkins_root
        Labels - DOTNET_7
        Usage - onelu build jobs with label exp.....
        Lanch method - Launch agents via SSH
            Host - Pravite IP of node-3
            Credentials - ubuntu (this is my key for ububtu)
            Host key verfication stratehy - Non verifying verfication
--(SAVE)--
--(BUILD NOW)---

    ^ cd /tmp/
    ^ cd nopCommerce-july23/
    ^ git branch
    ^ dotnet restore src/NopCommerce.sln
    ^ dotnet build src/NopCommerce.sln
            :MSBuild version 17.4.8

* For day builds
* dotnet build  -c "Debug" <path of project or sln>
* For night builds
* dotnet build  -c "Release" <path of project or sln> 
------------
------------

### NopCommerce building in (APS)
    crate a vm (AMI - location 20.04 )- 
                (instant type : t2- mediam)
    open APS - 
        open web(dotnet install ubuntu) - (https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2004)
        (NOTE 20.02)
   ^ Copy - Add the Microsoft package repository - command
   ^ copy - Install the SDK - command
   ^ sudo apt install openjdk-17-jdk -y
   ^ cd /tmp/
   ^ git clone https://github.com/runtiru/nopCommerce.git
   ^ cd nopCommerce/
   ^ dotnet restore src/NopCommerce.sln
   ^ dotnet build src/NopCommerce.sln

### NopCommerce Manually run....?
    


---------------------------------
# 21/07/23...
---------------------------------
### Upstreem and Downstreem projects:
    Login jenkins with jenkins_master IP
Create a + New View
        NAME - Experimental
        TYPE - List view
    --(Create)--
    (NO need to add any options)
    --(OK)--

Create + New Item
    Neme - projeci A
    free style project
    --(OK)--

General - This is project A
Build steps - 
    (add build step)
    Execute shell
        Command - echo "project A"
    --(SAVE)--
---------
Create + New Item
    Neme - projeci B
    free style project
    --(OK)--

General - This is project B
Build steps - 
    (add build step)
    Execute shell
        Command - echo "project B"
    --(SAVE)--
------------
Create + New Item
    Neme - projeci C
    free style project
    --(OK)--

General - This is project C
Build steps - 
    (add build step)
    Execute shell
        Command - echo "project C"
    --(SAVE)--

## Create a link of these 3 projects
   Goto project A configure
Post-build Acitons
    Build other projects
        projects to build - project B
    --(SAVE)--
------
    Goto project C 
Build Triggres
    Build after other projects are built - Project B
    --(SAVE)--
------
# How to Sleep your projects
General - This is project A
Build steps - 
    (add build step)
    Execute shell
        Command -   echo "project A"
                    sleep 10s
    --(SAVE)--
SAME ALL 3 PROJECTS...
    Now Build scheduled of project A - once project A build -- automatically B and C updated....
------------------------
## Parametrized Builds  -----> RT (15:00)
    Start node-2 (ubuntu instant)

Create a + New View
        NAME - Serious
        TYPE - List view
    --(Create)--

    JOBS
        select gameoflife
        select nopcommerce
        select spc-day build
    --(OK)--
Goto Serious---->
    gameoflife - configure
Build sieps
    incoke top-level maven targets
        Maven version - MAVEN_DEFAULT
        GOALS - package
General
    Description -
        select This project is parameterized
        (Add parameters)
            choice parameter
                NAME - GOAL
                CHOICE -    compaile
                            package
                            install
                            clean package
                            clean install
Build steps
    Goal - $GOAL (remove the package)
    --(SAVE)--
Build with perameters
    Goal - clean package                 
    --(DULD)--                   

## ## Jenkins Environmental variables: -----> RT (24:00)
*   Jenkins injects environmental variables into every job in addition to environmental variables present on node:-
*   view environmental variables Naviage to build steps => execute shell 

    on node-2 copy public IP
            open APS
                ^ ssh ununut@past IP
                ^ printenv  --- (its show some environmetal varebuls)
* goto Experimental project:-
    Craete a new project (+ New Item)
        Name - environmentalvariablesdemo
        free style project
    --(OK)--
    General
        JDK  - JAVA_8
        Select Restrict where this project can be run
            Label Expression - JDK_8
    Build steps 
        (Add build step)    
        Execute shell - printenv
--(SAVE)--
--(BUILD NOW)--

## Find Environmental variables:-
    goto any project 
        in build steps 
           exeucute shell 
                (the list of available environment aratables)
                (OR)
goto website - find to jenkins useing envitonment variables
    {https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables}


## Sample using environmetal variables 
    goto any project ----> (environmentalvariblesdemo)
        in build steps 
           exeucute shell 
                (the list of available environment aratables)

    echo "Hello, This is project's url id ${JBB_DISPLAY_URL} and the build id is ${BUILD_ID}"
    echo "This project is running in folder ${WORKSPACE} on Node ${NODE_NAME}"
--(SAVE)--
--(BUILD NOW)--
            see console output --- echo hello,..............
                                    echo this project ..............

## How to take backup of jenkins
    goto manage jenkins
        plugins
            available plugins
                hear search for "backup"
                    "Periodic Backop"
* One option for backup of configuration files
    manage jenkins
        Uncategorized
            Periodic backup manager
                configure
    in configure
        Temporary Directoty - /tmp/jenkins
        Backup schedule - 5 23 * * *
        Maximun B I Loction - 5
    file management sreategy
        fullbackup
            follow symbolic links
        (ADD STORAGE)
    Storage Strategy
        Backup laoction
            local directory
                Backup directory path - /tmp/masterbackup
                Enable this loction
    --(SAVE)--
    Backup Now!

## Monitoring jenkins
### Which plugin should be installed to monitor jenkins
    -goto web - jenkins monitor plugin
        How to install

    -comeing to jenkins
        Dashboard
            Managejenkins
                Plugins
                    Available plugins
                        search for "monitoring"
        select monitorion
            install without restart
        Download progress
            select reast jenkins when installation is complete......
    --RESTART--
    Dashboard
        Managejenkins
            Monitoring of jenkins instance

* Jenkins Plugins can be installed from
       * Market place
       * Uploading the plugin

* Jenkins plugin has two extensions
    * jpi (Jenkins plugin interface)
    * hpi (hudson plugin interface)


---------------------------------
# 22/07/23...
---------------------------------
## ## 
## ## Pipeline as Code:---

    * This is expressing CI/CD pipleine in terms of some code/expressions/statements
    * This is part of version control i.e. each change done to the steps will have history

----------
*   Jenkins has two flavours
        1. Scripted Pipeline - This was developed where you can execute groovy language directly.
        2. declarative Pipeline - Jenkins has created a DSL (Domain specific Language) which is mostly inspired from traditional jenkins.
   
### Create a Scripted Pipeline ---------->RT(20:00)

        Install jenkins in jenkins-master-node (IP:8080)
     1.   Create a +New view
            Name - Scripted, - List view, --create--
    --(OK)--
     2.   Create a +New view
            Nane - Declartive, - List view, --create--
    --(OK)-- 

Scripted 
---------
* Create a +New Item
    Name - gol-scripted-pipeline
    Project - Pipeline
--(OK)--
    Pipeline
        Definition
            Pipeline script
    -- Open pipeline syntax --

* Snippet Generator
    Overview
        steps
            sample step -----> (1
                select - node: Allocate node 
                         Label - JDK_8
        (Generate pipeline script)
            -copy the script-
-- paste in (gol-scripted-pipeline)---
---------
    node('JDK_8') {
        stage('git') {

        }
    }
---------
            sample step -----> (2
                select - git: Git  ----> copy - gameoflife git repo URL
            git
              Repo - (paste - gameoflife git repo URL )
              Branch - master
        (Generate pipeline script)
            -copy the script- 
-- paste in (gol-scripted-pipeline)---
-----------------
    Ex:-('node(`JDK_8`)) {
        stage(`git`) {
            git branch: `master` , url: 'https://github.con/dummyrepos/game-of-life-jely23.git'
         }
        stage(`build`)
    }
-------------------
            sample step -----> (3 -------------------> RT(34:00)
                select - maven (there is no found)
                select - shell script
                    mvn package
        (Generate pipeline script)                                
            -copy the script-
-- paste in (gol-scripted-pipeline)---

            sample step -----> (4
               select - archive: Archive artifacts
    gameoflife configure - archive the artifacts "copy the file to archive"
        archiveArtifacts artifacts: `**/gameoflife.war` , followSymlinks: false

            sample step -----> (5
                select - junit: Archive JUnit-formatted test results
    gameoflife configure - publish junit result report "copy test report XMLs"
            "paste jenerste pipeline "
           "junit '**/surefire-reports/TEST-*.xml'" 

-------------------
1   node('JDK_8') {
2       stage('git') {
3           git branch: 'master' , url: git 'https://github.com/wakaleo/game-of-life.git'
4       }
5       stage('build') {
6           sh 'mvn package'
7       }
8       stage('reporting') {
9           archiveArtifacts artifacts: '**/gameoflife.war', followSymlinks: false
10          junit '**/surefire-reports/TEST-*.xml'
11      }
12  }
-------------------
-------------------
### Create a Declartive Pipeline:------------>RT(40:00)

    Start node -1 instant (spc-day-build)
 In Jenkins - spc-day-build ---> configure
    check what we are done...!

Declartive Pipeline:-
--------------------
* Declartive
        * Create a +New Item
    Name - spc-declartive
    Project - Pipeline
--(OK)--

* We have written
    Pipeline
        Definition
            Script..?
    sample step -----> (1
        select - node: Allocate node 
                 Label - JDK-17

    sample step -----> (2
        select - git: Git
    (copy URL of spc-day-build)
    (paste the URL and what is branch)
(Generate pipeline script)

    sample step -----> (3
        build
            mvn package
----------------------
[Title](<Scripted and Declartive pipeline>)
----------------------

### Scripted Pipeline -------------> RT (01:17:00)



### Declarative Pipeline:- -----------> RT (01:28:00)
*  create a DP by exploring most options in DP:-
-------------------------------------------------
    In APS:
Create a file - temp/Jenkins/
    ^ git clone (spring-petclinic-1.github http:ID)
* create a develop branch

    ^ cd spring-petclinic1
    ^ git branch 
    ^ git checkout -b develop
    ^ git push -u origin develop
    ^ code .     ---> create a VSC New file (create a new file - name Jenkinsfile)

activate node-1 (name - runner)
activate jenkins_master node
```bash
pipeline {
    agent { any, none, label, node, docker }
    environment { - }
    options { buildDiscarder, checkoutToSubdirectory, disableResume, retry, skipDefaultCheckout, timeout }
    triggers { cron, pollSCM, upstream }
    tools { maven, jdk, gradle }
    stages {   
        stage('vcs') {
            steps  {--------(1
            }
        }
        stage('build and package') {
            steps  {--------(2
            }
        }
        stage('reportion') {  
            steps  {--------(3
            }
        }}

}
```
* Pipeline Steps Reference - search what need you want for project..
    1. git
        Git plugin - git: Git
            - Argument Descriptions (url, branch, changelog, credintialsID, poll )

    stage('vcs') {
            steps  {
                git url: (spc1 url),
                    branch: 'develop'
            }
    }
    2. maven
(if you dont find any thing - you can search 'shell') 
        Pipeline: Nodes and Processes
            sh: Shell Script - (script, encoding, label, returnstatus, )

    stage('build and package') {
            step {
                sh: Script: 'mvn package'
            }
    }

   3. archive artifacts
          Jenkins Core
            aA: Archive the artifacts
                archiveArtifacts -(artifacts, ....) 
            junit
                JUnit Plugin
                    junit: Archive JUnit-formatted test results
                        (testResults, .....)
    stage('reporting') {
            step {
                archiveArtifacts artifacts: '**/target/springpetclinic-*.jar'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
-------------------------
## We have developed the basic skeleton

```bash
pipeline {
    agent { label 'JDK-17' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_17'
    }
    stages {
        stage('vcs') {
            steps {

            }
        }
        stage('build and package') {
            steps {

            }
        }
        stage('reporting') {
            steps {

            }
        }
    }

}
```
-----------------

        ^ git add .
        ^ git commit -m "Added daybuild for jenkins in declartive fashion"
        ^ git push

*  "change spingpetclinic branch master to dovelop" ----------->RT(02:02:00)
    in jenkins declartive - spc declartive - configure
        pipeline
            definition 
                pipeline script from SCM
                    SCM - Git
                        repository URL - spchithub urlID
                        branch - develop
                    Script Path
                        jenkinsfile
    --(SAVE)--
  --(BUILD NOW)--

if any errors 
    change what is error and
        ^ git add .
        ^ git commit -m "added daybuild for jenkins in declarative fashion"
        ^ git push
------------------


--------------------
## 23/07/23
--------------------
### Declartive contd

        Activeate jenkins_master node 
        manage jenkins node-2 activate ('JDK_8')
    copy the gameoflife repo url (https) ----(game-of-life-july23)
 
in terminal 
    ^ cd C:\tmp\jenkins\
    ^ ls
    ^ cd spring-petclinic-1
    ^ git clone (paste the url of gol)
    ^ cd .\game-of-life-july23\
    ^ code .   ------> (vsc)

in vsc - create a file "jenkinsfile"
```bash
    pipeline {
        agent { label (JDK_8) }
        environment { - }
        options {
            retry(3)
            timeout(time: 30, units: 'MINUTES')
        }
        triggers {
            pollSCM('* * * * *')
        }
        tools {
            jdk 'JDK_8'
        }
        stages {
            stage('source code') {
                steps {
                    git url: 'copy the gol github url',
                        branch: 'master'
                }
            stage('package') {
                steps {
                    sh script: 'mvn clean package'
                }
            }
            stage('reports') {
                steps {
                    junit testResults: '**/surefire-reports/TEST-*.xml'
                    archiveArtifacts artifacts: '**/target/fameoflife.*war'
                }
            }  
        }
    }
}
```

    ^ git status
    ^ git add .
    ^ git commit -m "Added pipeline"
-----------
what ever projects run than desables now...!

goto jenkins
    Scripted
        gol-scripted-pipeline - configure -------- Disabled project.--save--.

Serious projects
------------

* create gameofline project
-----------------------------
    in Declartive
        --New Item--
            name - gemeoflife-diclarative
                general - 
                pipeline - Difenition - Pipeline script from SCM
                    SCM - Git
                        repository URL - (git gol url)
                    branch - master
    ^ git add .
    ^ git commit -m "Added pipeline"
    ^ git push
    
    --save--
 --Build now-----------------> RT(22:00)
 
    ^ git log --oneline
seen how many mistackes we done
    ^ git rebase -i HEAD~2   -----> combind all to ine commit
            do chenge to
        - give 's' its mens change your commits 
    
-----
### Email Notifications ----------->RT(30"00)
------------------------
    login 'mailtrap' and active project & nodes
        in mailtrap 
            create one inbox (Add inbox - name - jenkins)
                in that jenkins "show credentials"
-------->
Pipeline Steps Reference
    search - mail
        Pipeline: Basic Steps
            mail: Mail
subject:
body:
bcc:
cc:
from:
to:
--------->

     goto the jenkins project 
        Dashbord
            Manage jenkins
                system
                    E-mail Notification
                        SMPT sever - sandbox.smtp.mailtrap.io (mailtrap jenkins smtp host:)
                        Default user e-mail - noneed
                        (Advanced)
                            user name - 133e7a1c941595 (mailtrap jenkins smtp host)
                            password - 76c3c01874012a
                        use TLS (select)
                        SMTP Port - 587
                        Test configuration by srnding test e-mail
                            info@test.com (if this email is currect msg will send)
        --Test configauration--
    --save--

* if your project has been success:-

        stages {
           stage('reports') {
                steps {
                    junit testResults: '**/surefire-reports/TEST-*.xml'
                    archiveArtifacts artifacts: '**/target/fameoflife.*war'
                }
            }
        }
        post {
            success {
                mail subject: "your project is effective",
                     body: "your project is effective",
                     to: "all@qt.com"
            }
        }

* if your project has been faild:-

        post {
            failure {
                mail subject: "your project is defective"
                     body: "your project is defective"
                     to: "all@qt.com"
            }
        }
* how i do that mail
--------------------
    gameoflife-declartive - project after success
            Replay ----(in the console output)
                remove old script and paste the what you write (project are success or failure)
   --RUN--

        Now see the mail (mailtrap)
            ( project are success or failure )
once done 
        ^ git add .
        ^ git commit -m "Added mail notification jenkins"
        ^ git push
---------------------

## Microsoft teams/slack notification ----------->RT(43:00)

    in web "notification to teams from jenkis" 
        --https://identicalcloud.com/blog/how-to-send-notification-to-microsoft-teams-from-jenkins/--


## Parameters from jenkinsfile:- -------------RT(01:19:00)




## User Administration in Jenkins:- ---------RT(01:27:00)


----------

### jfrog

### sonar cube