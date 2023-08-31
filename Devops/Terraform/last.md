## 27/08/23
-----------
### Problem Statement
----------------------
Create one vm (instance)
   - install jdk-17   ---> for node configure
    * terraform install
        - terraform --version 

    * aws cli install
        - sudo apt install unzip 
        - aws configure (cat ~/.aws/credentials)
            (note: give region also)
    
    * jenkins
        - add node (infreprovisnor)
        - create new item - freestyle/pipeline (aws-tf-example)
        <!-- - (copy the VPC ID after success project) -->

    * AWS Cloud formation
        - json
        resources
    <!-- * aws cloudformation create stack -->
^ aws coludformation create stack--stack-name <--> --template-bldy <--> "file .\main.json

    * create one more jenkins freestyle project for cloud formation



