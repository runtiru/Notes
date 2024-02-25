## 10/17/23
-----------
Azure DevOps
------------
    - Also called Visual Studio Team Services
* Servies:
    - manage agile projects
    - test management
    - Pipelines

* Features:
    - Devloping
    - Testing
    - Operations (Pipeline)
    - Managment (project)

* Azure DevOps setup
    - Azure DevOps Server:
        We need to install this on Windows Servers

    - Azure DevOps Services
        This is already hosted
        We can create account using
            GitHub
            Microsoft Account

* Services offered
    - Wiki: For documentations
    - Boards: Here the whole project items
        product backlog
        sprint backlogs
        burn down charts …
        Scrum board
    - Azure Repos: This is to manage source code
    - Azure Pipelines: This is to manage CI/CD pipelines
    - Azure Test Plans: Test management i.e. Test cases, executions, defects and reports are managed here
    - Azure Artifacts: Storage for packages build during pipelines.

==========================================================
## 21/10/23
### Building and Packaging Java Projects using a Maven
[https://directdevops.blog/2023/10/21/devops-classroom-notes-21-oct-2023/]
* Compilation:
(High level to low level before executing the application.)
   - checks for errors in code
   - converts to desired language (Byte code/machine code)

* Packaging:
   - Combining compiled code into some packaging format
      java: jar/war/ear
      dotnet: dll/exe

* Dependencies: will be downloaded
    java: maven/gradle
    dotnet: nuget
    python: pip
    nodejs: npm

# Maven:-
    - combines dependency resolution, compilation, unit test executions, packaging

* Maven expects a file called as `pom.xml`

* Steps:
    * Get the latest code
    * Pre-requisites:
        - jdk version
        - maven
    * Execute mvn <goal>
        - compile
        - test
        - package

    * In our case we will be using `mvn package`

# Setup a linux vm for building and packaging spring-petclinic
  * pre-req’s
        git
        maven
        jdk 17
  
  * SSH into the vm & execute the following
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install maven -y
git --version
java -version
mvn --version
```

* Build steps
```bash
cd ~
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
mvn package
```

## Azure DevOps Pipelines
* Azure DevOps has two ways of building pipelines
    1. Classic Pipelines: We rely on user interface
      - Drawback:  History will be missing
      - Advantages: Easy to start.

    2. Azure Pipelines YAML: Pipeline as Code. We will define pipelines steps in a file `azure-pipelines.yaml` and add it to the version control system (git)
      - Advantage:  History will be maintained
      - Disadvantage:  Learning curve for writing pipeline


# Azure DevOps has agents:
*  Agent is where the build is executed.
    There are two types of agents
    1. Microsoft Hosted agents: These are machines which will be created on demand by Azure DevOps and will be delete upon build completion.

    2. Self Hosted Agents: These are machines managed by us, we add these machines as agents to Azure DevOps.

## Configuring Spring petclinic build on Azure DevOps

* Create a Repositorys
    Repos --> files --> projectname --> import repository --> paste the git url.. > import

* change branch 
    Repos --> Branches --> main --> set a default branch

* SetUp Build....
* Configure your pipeline
(what is your project - maven (build))

* Review
    change jdkversionoption: '1.17'

--> `save and run` <--

========================================================================
## 22/10/23
### Configuring Self Hosted Agent in Azure DevOps
[https://directdevops.blog/2023/10/22/devops-classroom-notes-22-oct-2023/]
* Self Hosted Agent is the linux/windows/mac instance managed by us

* Configuring Self hosted agents
    Linux Refer Here
    Windows Refer Here
    
* To maintain collection of Agents, Azure has Agent pools. By default we will have two pools
    - `default`: for self hosted agents
    - Azure Pipelines: for Microsoft hosted agents
* Lets create a ubuntu linux vm and as discussed in the session install, configure and run the agent

* Agent --> Project settings --> Agent pools --> `Default` --> Agents --> new agent -->  Linux --> Download the agent

* install vm (medium)
    ^ cd /tmp/ (reasion - once the machine restart delete automatically)
    ^ wget <paste download agent ip>
    ^ cd ~
    ^ mkdir myagent && cd myagent
    ^ tar -xvzf /tmp/vsts-agent-linux-x64.................
    ^ ls
(some .sh folders...)
    ^ ./config.sh

    ^ yes
server URL
[https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/windows-agent?view=azure-devops]
    Eg: https://dev.azure.com/{your-organization}.
    ^ https://dev.azure.com/runtiru7799 (this is my server URL, every new project its changes...)

    ^ Enter personal access token > **********************************************
check what ever you want...

    ^ ls
(som .sh foleders are created 
 _diag  bin  config.sh  env.sh  externals  license.html  run-docker.sh  run.sh  svc.sh)
here `run.sh & svc.sh`
    run.sh -> it's exucte one time run once 
    svc.sh -> it's exucte once its run all the time untill you stop

    ^ ./run.sh


# Personal Access Token
-> user settings --> Personal Access Tokens -->new token -- name -- (full access) --> crate token --> copy the token some where (once close the token was deleted so save some where...)


now go to Repos -> azure-pipelines.yml -> change 
```bash
trigger:
- main

pool: default

steps:
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: 'mvn package'
```


==========================================================
## 27/10/23
### Azure DevOps YAML Schema
[https://directdevops.blog/2023/10/27/devops-classroom-notes-27-oct-2023/]
    - The pipeline as a code is represented in a file called as `azure-pipelines.yaml`.

* Azure Pipelines is collection of
    Stages:  Each Stage is collection of Jobs
        Job:  Each job is collection steps
          Step: A unit of activity

# Lets create a pipeline for java project:-
* Manual steps:
refer [https://directdevops.blog/2023/10/21/devops-classroom-notes-21-oct-2023/]

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install maven -y
git --version
java -version
mvn --version
```
* First Version (Stage,job and steps)
```bash
---
pool: default
stages:
  - stage: 'buildstage'
    displayName: Build and Package using Maven
    jobs:
      - job: 'buildjob'
        displayName: 'Build the application using Maven'
        steps:
          - bash: 'mvn pacakage'
---
```
* Second Version (Job and steps)
```bash
---
pool: default
jobs:
  - job: 'buildjob'
    displayName: 'Build the application using Maven'
    steps:
        - bash: 'mvn package'
---
```
* Third version (steps)
```bash
---
pool: default
steps:
  - bash: 'mvn package'
```

# Azure DevOps Steps
 * Types of Steps
    task: reusable build/deploy/utility steps
    script: Runs a script using cmd.exe on Windows and Bash on other platforms.
    powershell: Runs a script in a powershell
    pwsh: Runs a script in a powershell core
    bash: Runs a script in a bash shell
    download
    downloadBuild
    getPackage
    publish
    template
    reviewApp

# Try to open VSCode this file
    --> clone SSH <git@ssh.dev.azure.com:v3/runtiru7799/Az_Dev/spring-petclinic.git>
    --> give manage ssh key


* We have started using Maven Task
```bash
pool: default

steps:
  - task: Maven@4
    inputs:
      mavenPOMFile: pom.xml
      goals: package
      publishJUnitResults: true
      testResultsFiles: '**/TEST-*.xml'
      javaHomeOption: Path
      jdkVersionOption: '1.17'
      jdkDirectory: '/usr/lib/jvm/java-17-openjdk-amd64'
      mavenVersionOption: Path
      mavenDirectory: '/usr/share/maven'
```

    ^ whereis java
java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1.gz
    ^ ls -al /usr/bin/java
lrwxrwxrwx 1 root root 22 Nov  7 06:45 /usr/bin/java -> /etc/alternatives/java
    ^  ls -al /etc/alternatives/java
lrwxrwxrwx 1 root root 43 Nov  7 06:45 /etc/alternatives/java -> /usr/lib/jvm/java-17-openjdk-amd64/bin/java
    `/usr/lib/jvm/java-17-openjdk-amd64/bin/java`

    ^ whereis maven
mvn: /usr/bin/mvn /usr/share/man/man1/mvn.1.gz
    ^ ls -al /usr/bin/mvn
    `/etc/alternatives/mvn`


===========================================================================
## 28/10/23
### Build a dotnet application:
    Project: NopCommerce [https://github.com/nopSolutions/nopCommerce]
    Branch: master
    Pre-req’s:
        - git
        - dotnet 7 sdk
[https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204]

```bash
sudo apt-get update && \
sudo apt-get install -y git dotnet-sdk-7.0
```

* Manual steps:
```bash
git clone https://github.com/nopSolutions/nopCommerce.git
cd nopCommerce
git checkout master
dotnet build src/NopCommerce.sln -c Release
dotnet test -c Release src/Tests/Nop.Tests/Nop.Tests.csproj -o TestResults/
dotnet publish src/Presentation/Nop.Web/Nop.Web.csproj -c Release -o published/
```

* Dotnet projects: have two modes of building
    Debug
    Release

* Command refernces
    build: [https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-build]
    test: [https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-test]
    publish: [https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-publish]

# Azure DevOps Pipeline
    - Our agent is still default
    - build steps

```bash
dotnet build src/NopCommerce.sln -c Release
dotnet test -c Release src/Tests/Nop.Tests/Nop.Tests.csproj -o TestResults/
dotnet publish src/Presentation/Nop.Web/Nop.Web.csproj -c Release -o published/
```

* When should the project be built
    - ption 1: Whenever code is pushed to some branch
    - option 2: At schedule time
    - option 3: On Pull Request

* Sections in Azure DevOps pipeline yaml
    - trigger (option 1) Refer Here
    - schedules (option 2) Refer Here and Refer Here
    - pr (option 3)

* Crontab Refer Here
* Pipeline which i have built so far

```bash
---
pool: default

trigger:
  - master

steps:
  - task: DotNetCoreCLI@2
    inputs:
      command: build
      projects: src/NopCommerce.sln
      configuration: Release
  - task: DotNetCoreCLI@2
    inputs:
      command: test
      projects: "**/*.Tests.csproj"
      publishTestResults: true
```

==================================================================
## 29/10/23
### Azure DevOps Pipelines
* Pipeline is collection of stages and stage is collection of jobs and job is collection of steps.

* Stage: This represents a logical activity in ci/cd pipelines, examples: build, test, deploy. Each stage can be executed on a different agent

* In one stage we can multiple Jobs and if required they can run in parallel.

# Variables in Azure DevOps Pipelines
