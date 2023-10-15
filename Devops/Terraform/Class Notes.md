--DELETED--

--------
27/07/23
--------
        --installations--    

-----------
## 08/08/23
-----------
Creating a RDS database in aws:-
--------------------------------
## Manual steps:
create a RDS instans:

    * inputs: 
        --class room notes--

Resource
* Argument reference
        
-----------
## 09/08/23
-----------
## create a database (ntier - aws)
  * steps
        - generate key pair (import key pair)
        - create on ubuntu instance (figyre out ami if for os)
link with APS
        ^ sudo apt update
terminate instance
delete key pair also


VSC :- create appsrver.tf
--------------------------

resource "aws_key_pair" "private" {
        key_neme = "ntire"
        public_key = file(")
}

inputs.tf
---------

appserver.tf
-------------

----xxx------

## 12/08/23 - terraform workshop
--------------------------------
* Provisionesr in terraform:- 

    Local - the mactine wher you create
    Remote - this executes in resource created by terraform

## nitre - aws. Install apache in ce2 
    * manual steps (apache)
        
    'Install jenkins in remote mactine'

Ex:-
connection {
    type = 
    user = 
    password = (use public or private ip)
    host = self.public_ip (when you give public ip )
    
    provisioner "remote
}
 
* create one folder - 'inatalljenkins.sh' in vsc
    (install all jenkins commands)

#!/bin/bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
sudo apt install jenkins -y

    ^ terraform fmt
    ^ terraform validate
    ^ terraform apply

NOTE:- ??????

-----
## Relizing using terraform
terraform
git clone https://github.com/asquarezone/TerraformZone.git

# aws
    ^ cd july23/ntier-aws
    ^ terraform init
    ^ terraform apply -var-file="dev.tfvars"

-->

null resource 
    triggers
----------------

**AFTER BREAK** 

My activity
    * tey to create one ec2 and install apache useing terraform...

----

## Concept - backend 
    * tf by default stores the state lically so multi user exection will create problems.
    * the default backend is local backend.

-----
-----

## 13/08/23
# Next steps:
    * Backend
    * Workspace
    * Modules and registry
    * State managment:
        - inport
        - state loss scenarios


can you explain 
    what is terraform
        what is arguments
        what is attributes
        what is resources

---
## ntier-aws

    terraform workspeace....?

-----------
## 16/08/23
-----------
### Create vpc in south 

            cross check work or not:-
                    ^ aws ls 
                    ^ terraform --version
+ create one folder in pc
    ^ terraform init
    ^ 
* provider.tf
-------------
terraform {

}
-----

* vpc.tf
--------
module "vpc" {

}
-----

after add 
    ^ terraform fmt
    ^ terraform apply
    -yes-
login to aws check....??

## Concepts:-
### terraform modules
----------------------
    - reuseble terraform template
    - terraform registry is collection of public modules
    - 

* securitygroups.tf
-------------------
resource "--" {

}

+ create new folder (modules)
    in modules - one folder securitygroup open to 
VSC:-
* inputs.tf
-----------
variable "--" {

}

* main.tf
---------
resource "--" {

}

* outputs.tf - web-terraform outputs
------------
output "--" {
    value = aws_security_group.sg.id
}

move to modules in APS
    ^ terraform 
    ^ terraform fmt

+ create onemore folder (moduledemo)
* main.tf
module "securitygroup" {
    source = "./modules/securitygroup"

}
-----
* providers.tf
terrafotrm "--" {

}
-----
    ^ terraform init
    ^ terraform fmt
    ^ trerraform validate
    ^ terraform apply
    -yes-
created new security groups


## GitHub.com:-
---------------
