----------
# 26/07/23
----------->
* Create a infrasture (or)
  Create a instanece (linux machine) - manully - crosscheck to APC
    and 
install apache sever
    ^ sudo apt update && sudo apt install apache2 -y

crosscheck apache server
        copy the instant (public ID)
    goto web paste the ID - check the apache2 default page

----------->
## Create an instance useing terraform:-

    Creatr a folder 
         "open vcs to awsec2 folder"
in VCS
    create a file - providers.tf
(terraform provider syntax)
in web - https://registry.terraform.io/providers/hashicorp/aws/latest/docs

* providers.tf
-------------->
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.11.0"
    }
  }
}

provider "aws" {
  * Configuration options 
}

---->
(remove # Configuration options)
and region - where your instance in that region..
---->

provider "aws" {
  region = "us-west-2"
}

# add resource (aws_resource)
* how to write a syntax :- Argument Reference of terraform aws providers docs

* main.tf
---------
resource "aws_instance" "---" {
  ami                    = "---"
  instance_type          = "t2.micro"
  key_name               = "N.V_key"
  vpc_security_group_ids = ["sg----"]

  tags = {
    Name = "---"
  }
}
-----> 
in APS:-
    ^ terraform init
    ^ aws configure
(create IAM and give access key permitions)

    ^ terraform fmt
    ^ terraform validate
    ^ terraform apply
   -yes-
in instance - refresh - now create one instance automatically 
---------
----XX----
* provider.tf:-
---------------
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.11.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"
}
* main.tf:-
-----------
* main.tf
---------
resource "aws_instance" "---" {
  ami                    = "---"
  instance_type          = "t2.micro"
  key_name               = "N.V_key"
  vpc_security_group_ids = ["sg----"]

  tags = {
    Name = "---"
  }
}
----xx----
----------

## Architecture of Terraform ---->RT(15:00)
------>
## Concepts of Terraform---------->RT(25:00)
------>
* List of AWS Provider:- This determines the target area to create infra structure
   Refer:- https://registry.terraform.io/browse/providers (list of providers)

* Terraform providers are of three categories
    Official
    Partner
    Community
------
* same instant create on terraform..! 
    (web -> terraform aws provider aws (or) 
    Refer:- https://registry.terraform.io/providers/hashicorp/aws/latest/docs) 
-------
* Arguments and Attributes:---------->RT(29:00)
    * Argument Reference to inputs in terraform
    * Attributes Reference to outputs in terraform

----------
# 27/07/23
-----------
## Infrastructuer as a Code :-

## Infra Provisioning:-

## Terraform:-

## Syntaxes in Terraform:-
        --Installations--
after installations----> RT (58:00)

----xx----

* Create a folder (Name = "---")
    ^ terraform init

VCS:-   ---->RT(59:00)
    
(NOTE: Do select auto save mode (file - auto save))
               
----------
# 28/07/23
----------
##   Create S3 account in AWS (manual)
        login AWS - S3

* Resource
  * S3 (simple storage service (S3))
        + create bucket
            General configuration
                Bucket name - forlearninginqt
                AWS Region - US East (N. Virginia) us-east-1
    --Create bucket--

### Infra Provisioning using terraform.
## Create a S3 bucket using terraform....

* Create an empty folder in pc -

open with VSC...
    In VSC create a file - Name - provider.tf
    
* Terraform aws Provider docs - https://registry.terraform.io/providers/hashicorp/aws/latest/docs
    _- "use provier" and copy the sample syntax

* provider.tf:-
--------------
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.11.0"
    }
  }
}

provider "aws" {
    region = "---"
}
--->

* Inputs --> Arguments 
* Outputs --> Attributes

* Authentication and Configuration (aws create in 6 diffent ways)
        1. Parameters in the provider configuration
        2. Environment variables
        3. Shared credentials files
        4. Shared configuration files
        5. Container credentials
        6. Instance profile credentials and region

* Basic user cration of IAM - https://directdevops.blog/2023/07/27/aws-classroomnotes-27-jul-2023/

### Create an IAM (manual)
 https://sst.dev/chapters/create-an-iam-user.html

(## IAM   --------RT(17:00)
    Create one user - name - "---" (any name)
        next
            Attach policies directly
        Policy name - 
            AdministratorAccess
                next
                -create user-
        
    select terraform
        security credentials
            Access keys
                Create access key
                    ues case - Command line inserface
                    Confirmation select
                        next
                     create access key
           
    ( access key  &  secret access key )
   dont share your access key and secret key

*    goto arguments (in Provider docs ))

---->(2
provider "aws" {
    access_key = "---"
    secret_key = "---"
    region = "---"
}
---->

now the provider is ready.....
--x--

in APS:-
    ^ cd open (what you create empty folder)
    ^ terraform --help
    ^ terraform init  ----> create a provider
    ^ terraform validate  ----> configaration validate../ "success"

before apply we need aws cli
    * Handling credenitals in AWS ------RT(36:00)
    * install aws cli
        after install cli - command 

    ^ terraform --help -----> what is the next step
    ^ terraform apply --help
    ^ terraform apply
(Apply complete! Resources: 0 added, 0 changed, 0 destroyed.)

open :- https://directdevops.blog/2023/07/27/aws-classroomnotes-27-jul-2023/
    search 'S3'
        S3 (simple storage)
            resources
                aws_s3_bucket
look out for -
     * Argument Reference
in VSC:- 
---->(3     
resource "aws_s3_bucket" "first" {
    bucket = "---" (this is the argiment name)
}
---->
(NOTE:- s3 always need new names)

in APS:-    -------RT(33:00)
    ^ terraform fmt
    ^ terraform validate               
    ^ terraform apply
   -yes-
    ^ terraform apply ---> again

goto S3 instance:
  -refress-
    see the 2 instances

select one and delete )

in APS:-
    ^ terraform apply
  -yes-

----------
# Fainal product:
----XX----
* provider.tf:-
---------------
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.13.0"
    }
  }
}

provider "aws" {
  access_key = "AKIA4IITGWPJK7RCGGXA"
  secret_key = "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"
  region     = "us-east-1"
}

* main.tf:-
-----------
resource "aws_s3_bucket" "tfs2" {
  bucket = "tfs23"
}

----xx----
---------
-----------------
-----------------

once done the work or activity in AWS -----RT(35:00)
    deactiveate the access keys
* IAM
    user 
        (name of IAM)
            security credentials
                Access keys
                    Action 
                        --Deactivate--
            and 
                -Delete-
---------------------
======================================

# Handling credenitals in AWS 
                            ------RT(36:00)
    * install aws cli
        after install cli - command 

    ^ aws configure

    open APS:-  
        ^ aws configure
        ^ AWS ACcess key - 
        ^ AWS Secret key -
        ^ Default region -
        ^ terraform apply
 ----

AWS:- 
    IAM - Access management
        user 
            -create access key-
    use case
        select command line interface
        -- confirmation and next--
        - create a key -

copy the Access key.....

    open APS:-  
        ^ aws configure

        ^ AWS ACcess key - 
        ^ AWS Secret key -
        ^ Default region - 
    
goto VSC - 
    remove old access key and secret key

goto APS -              -------RT(39:00)
    ^ terraform apply
    ^ 
    -Add- 
provider "aws" {
    access_key = "...."     
    secret_key = "...."
    region = "...."
}

### Create S3 in Azure..    -----RT(43:00)
--
--
--

----------
# 29/07/23
-----------
## Order of creations

    1. Explicit dependency:- (we are know and telling the dependency)
   
    2. Implicit dependency:- (you dont tell the dependency terraform will understand which is the dependency)

--->
## Explicit dependency
# create resource group in azure :-

    Create one folder in pc--
        inside the folder create (.tf) file
login to VSC-

add this resource--->

* provider "azurerm" {
    features {
    }
}

resource "azurerm_resource_group" "myresg" {
    name = "fromtf"
    loction = "eastus"
}

resource "azurerm_storage_account" "first" {
    name = "fromtfortf"
    resource_group_name = "fromtf"
    location = "eastus"
    account_tier             = "Standard"
    account_replication_type = "GRS"
    depends_on = [ azurerm_resource_group.myresg ]
}

goto APS:-
    move to what you create manuall file (khajaclassroom\devops\.........)

    ^ terraform apply
    -yes-
now created an azure resource group

    ^ terraform destroy

=====================================================

* 2. Implicit dependency ----RT(11:30)
-------------------------

create a folder

## Best practice to weite terraform template :- RT (23:00)

* terraform reads all the '.tf' files in the folder, and executes the terraform

* create this type of folders to read the ferraform 
        inputs.tf
        outputs.tf
         
    ^ terraform fmt (aline the terraform templare, its deals to )
    
## Manual step for next activity ------->RT (31:00)

   * Ntier Architecture in AWS
    ----------------------------


---------------------------------------------
## 29/07/23 -Jenkins workshop - evening class
---------------------------------------------

# Branching Strategy

* Git Flow:-
    * The main idea behind the Git flow branching strategy is to "isolate your work into different types of branches".
    * There are five different branch types in total:

    Git have Branches 
        Master (or) Main
        Develop
        Feature
        Release
        Hotfix

* The two primary branches - main and develop.
* There are three types of supporting branches: feature, release, and hotfix.

    1. Master Branch (version 1.0, 2.0 like)
            - any change on the masterbranch means that giving relese your coustmer (or) clint )
            - no developer will directly can submit the changes on masterbranch
            - masterbranch is rouldout
        - its create
          develop branch
            - any commit that are develop in develop
            branch represent that is done on developer
            - 

    2. Develop Branch  
            - its represent by individual developers
            - developers dont directly work on master branch
            - only do marge changes
        - its create
           feature/task branch (its not a part of git, its developer local laptops)
            - push the changes into feature branch
            - fast forword to frature branch
            
    3. Feature Branch/ Task Branch (Developers)
            - developr make the commits hear
    'developers changes the whant clint required'
            - once done the changes developer will 'marge' to develop branch

        -----> (Day Build)
    
    4. Release Branch
            - what ever changes done the develop branch to 'marge' to release branch
            - no one is working on relese branch

    - configure (Night Build)

        - you do build the code
        - you do static code analysis
        - you send to the package repo
    ance every thing done 
        - done test environment 
        - finally run automatiic test

    * once done all the changes we would relese the changes to coustmer

    5. Hotfix (iemedate fixes)
            - emergency changes 
            - fix the issues to release to master branch
    (3ways marge or cherry pic)

* refer to:- https://coderefinery.github.io/git-intro/basics/  

### Git lab branching strategies:-----RT(18:25)

- your branch represtnt your environment

    *. Master 
        - Deployed on staging (staging environment)
        - deploy to pre-production
        - 
    *. Pre-Production
        - deploy to production
        - 
    *. Production

## Pull-requsts -----RT(25:00)
---------------
    - it is a future of git repository
    
* GitHub.com
    (Install)

    - create a fork
*  add file (create new file)
    name - main.py
             (def main():
                pass)
    commit changes
        comit message - create main.py as this is required
    -ok-

this branch is 1 commit ahead of ...........


goto pull requst
    new pull requst
        base repo
            creat the pull requst


# Nop Commerce Pull request Based Workfolw ----RT(01:11:00)

# Git hocks

-----------
## 31/07/23
-----------
### ntier network in azure


## 02/08/23
------------
### ntier network in AWS:-
--------------------------
* create manual vpc (global region)
--------->>
* create iam (with add admistrative access)
------------------------------------------
  configure to what you create folder 
    ^ aws cinfigure
        aws access key:
        aws secret key:
    ^ terraform init (or) terraform init -upgrade (its mean your current version )
-success-
    ^ terraform fmt
    ^ terraform plan
    -yes-
    ^ terraform apply -auto-approve (or) terraform apply 
(ERROR)
    ^ terraform validate
    ^ terraform apply
    -yes-
------->>

* create an VPC (manual)
-------------------------
- Create VPC -
    VPC settings
        Resources to create - VPC only
        Name tag - optional - mnual
        IPv4 CIDR block - IPv4 CIDR manual input
        IPv4 CIDR - 10.100.0.0/16   (or) 10.10.0.0/16

    --create VPC--

in APS:-
    ^ cd c:\khajacalssroom\de......
    ^ git pull
    ^ git pull origin master
    ^
create one folder in - "ntier-aws"(khajacalssroom\devops\terraform\jely23)

    open VSC
        inside ntier-aws careate 
        - inputs.tf
        - main.tf
        - outputs.tf
        - providers.tf

in web 
    'terraform aws providers docs' - https://registry.terraform.io/providers/hashicorp/aws/latest/docs

use provider syntax :only terraform:
------------------------------------
* providers.tf:-
----------------
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = ">= 5.11.0"
    }
  }
  required_version = ">= 1.4.0"
}

provider "aws" {
    region = "is-west-1"
}
----->

in APS:
    ^ cd .\ntier-aws    (khajaclassroom\devops....)
    ^ terraform init
    ^ terraform fmt

    
------>
* find the VPC
---------------
    in web - 'terraform aws providers'
AWS DOCUMENTATION
        search vpc
            aws_vpc
(or)            
web- terraform aws vpc

* main.tf:-
-----------
resource "aws_vpc" "ntier_vpc" {
    cidr_block = "10.10.0.0/16"
    tags = {
        name = "ntier"
    }
}
---->
    ^ terraform fmt

* inputs.tf:-
-------------
variable "vpc_network_cidr" {
    type = string
    default = "10.10.0.0/16"
    description  = "this is network cidr"
}
---->
    ^ terraform fmt
--x--

* (some changes in main.tf)
    ---(NO NEED THIS CHANGES)---
resource "aws_vpc" "ntier_vpc" {
    cidr_block = "10.10.0.0/16" change to var.vpc_network_cidr
    tags = {
        name = "ntier"
    }
}
and create one file - "internals.tf" ----RT(16:40)

* internals.tf:-
----------------
locals {
    name = "ntier"      
                ----> in main.tf (name has been changed to "local.name")
}

------->

* if you got an error 
---------------------
    like - provider "aws" {}
do all the iam - user, terraform - init

## concepts of terraform
--------------------------
in web :
    terraform locals : https://developer.hashicorp.com/terraform/language/values/locals

in APS:
    ^ terraform validate
    success
    ^ terraform apply ----------> I HAVE ERROR - (becouse your iam is not run)
    yes                 -------->RT (19:00)
    ^ terraform --help
    ^ terraform show (values of instance)

    ^ git add .
    ^ git status
    ^ git commit -m "added vpc changes"

((now created vpc - name "ntier))
                        ------RT(38:00)
    ^ terraform show ---(execute)
    ^ terraform plan

onece create vpc 
    delete to manually
        re create on one click that is (command)
    ^ terraform refresh
    ^ terraform apply  --- (backup)
    
--------------
# final prduct
------XX------
* provider.tf:-
---------------
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.13.1"
    }
  }
  required_version = ">= 1.4.0"
}

provider "aws" {
  region = "us-east-1"
}

* main.tf:-
-----------
resource "aws_vpc" "ntier_vpc" {
  cidr_block = var.vpc_network_cidr

  tags = {
    Name = "ntier"
  }
}

* inputs.tf:-
------------
variable "vpc_network_cidr" {
  type        = string
  default     = "10.10.0.0/16"
  description = "this is network cidr"
}

* internals.tf:-
----------------
locals {
  Name = "ntier"
}

----xx----
---------

* what is provider..
* what is state
* what is main
* what is local
* what is inputs
* what is varaible
* how to difind a resource

# Lets add one subnet ----RT(57:45)
    8 Bits = 1 Bite
    cidr range: 10.10.0.0/16 to 10.10.255.255/

## Create a subnet:-(manual)
    Name = web 1

goto subnet
    create subnet
        vpc ID - vpc-0762ca....(manual)
      Subnet settings
        subnet 1 of 1
            subnet name = web 1
        Availability zone
            no preference
            10.100.0.0/24
    --create subnet--
---xx---

## subnet cterate in terraform:-
    open main.tf (vpc) -VSC
        create subnet in implicity dependency
web: terrafrom aws subnets (resources)
    refer: https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet.html

* main.tf:- (CONTD)
-------------
resource "aws_vpc" "ntier_vpc" {
  cidr_block = var.vpc_network_cidr
  tags = {
    Name = "ntier"
  }
}

resource "aws_subnet" "web1" {
  vpc_id     = aws_vpc.ntier_vpc.id
  cidr_block = var.web1_subnet_cidr

  depends_on = [
    aws_vpc.ntier_vpc
  ]
  tags = {
    Name = "web1"
  }
}

--->

* inputs.tf:- (CONTD)

variable "vpc_network_cidr" {
  type    = string
  default = "10.10.0.0/16"
}

variable "web1_subnet_cidr" {
  type        = string
  default     = "10.10.0.0/24"
  description = "This is web1 subnet cidr"

}
--->

    ^ terraform fmt

    ^ git status
    ^ git add .
    ^ git commit -m "added subnet"
    ^ git pushsub

    ^ terraform validate
    ^ terraform apply
   -yes-

* Exercise: Try adding 5 more subnets
-------------------------------------
    web1: 10.10.0.0/24
    web2: 10.10.1.0/24
    db1: 10.10.2.0/24
    db2: 10.10.3.0/24
    app1: 10.10.4.0/24
    app2: 10.10.5.0/24

-----------
## 03/08/23
-----------
### ntier-aws: adding 5 more subnets
-------------------------------------
* inputs.tf     (add this content middle)
----------- 
variable "vpc_network_cidr" {
  type        = string
  default     = "10.10.0.0/16"
  description = "this is network cidr"
}

variable "subnet_cidt_ranges" {
    type = list(string)
    default = [ "10.10.0.0/24", "10.10.1.0/24", "10.10.2.0/24", "10.10.3.0/24", "10.10.4.0.24", "10.10.5.0/24" ]
    desctiption = "This is network cidr ranges"
}

variable "subnet_name" {
    type = list(string)
    default = [ "web1", "web2", "app1", "app2", "db1", "db2" ]
    discription = "These are subnet names"
}

---
* main.tf ----(add middle)
----------
resource "aws_vpc" "ntier_vpc" {
  cidr_block = var.vpc_network_cidr

  tags = {
    Name = "ntier"
  }
}

resource "aws_subnet" "subnets" {
  count = var.subnet_count
  vpc_id = aws_vpc.ntier_vpc.id
}

--->

    ^ terraform console
      > var.subnet_cidr_ranges[0]
      > var.subnet_cidr_ranges[5]


      var.subnet_names[count.index]

######
* fainal project    ------RT(20:00)
######
* inputs.tf
-----------
variable "vpc_network_cidr" {
  type    = string
  default = "10.10.0.0/16"
  discription = "this is network cidr"
}


variable "subnet_cidr_ranges" {
  type        = list(string)
  default     = ["10.10.0.0/24", "10.10.1.0/24", "10.10.2.0/24", "10.10.3.0/24", "10.10.4.0/24", "10.10.5.0/24"]
  description = "This is network cidr ranges"
}

variable "subnet_name" {
  type        = list(string)
  default     = ["web1", "web2", "app1", "app2", "db1", "db2"]
  description = "This is subnet names"
}

variable "web1_subnet_cidr" {
  type        = string
  default     = "10.10.0.0/24"
  description = "This is web1 subnet cidr"

}

....>
-----------
* main.tf
----------
resource "aws_vpc" "ntier_vpc" {
  cidr_block = var.vpc_network_cidr
  tags = {
    Name = "ntier"
  }
}

resource "aws_subnet" "subnets" {
  count      = length(var.subnet_cidr_ranges)
  vpc_id     = aws_vpc.ntier_vpc.id
  cidr_block = var.subnet_cidr_ranges[count.index]
  tags = {
    Name = var.subnet_name[count.index]
  }
  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

....>
---------
* providers.tf
---------------
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.12.0"
    }
  }
  required_version = ">= 1.4.0"
}

provider "aws" {
  region = "ap-south-1"

}

....>
-------
## String interpolation:-
* what is string interplation
* how to do that in bash and powershell

   - An interpolated string expression creates a string by replacing the contained expression with the ToString represenation of the expression results.
        - vat test = $"City: {city}, area: {area}.";
    - replaced by name

* Ex:-  (gitbash)
    ^ $ name='DevOps'
    ^ $ echo "Hello DevOps"
       Hello DevOps
    ^ $ echo "Hello ${name}"
       Hello DevOps
    ^ name='AWS'
    ^ $ echo "Hello ${name}"
       Hello AWS

Ex:- (APS)
    ^ $name = "AWS"
    ^ Write-Host "Hello $name"
       Hello AWS
    ^ $name = "Azure"
    ^ Write-Host "Hello $naem"
       Hello Azure


-----------
## 05/08/23
-----------
* Terraform Functions:-
-----------------------
    - erraform functions are built-in, reusable code blocks that perform specific tasks within Terraform configurations.

 - refer:- https://developer.hashicorp.com/terraform/language/functions

Functions:-
    1. Numeric functions

    2. String functions

    3. Collection functions

    4. Encoding functions

    5. Filesystem functions

    6. Date & Time functions

    7. Hash & Crypto functions

    8. IP Network functions

    9. Type Conversion functions


### ntier-aws:
* fixing cidr range issue with terraform functions:-
    8. IP network functions
        cidrsubnet function
            cidrsubnet(prefix, newbits, netnum)

VSC:- (old)
    ^ terraform console
      > cidrsubnet("10.10.0.0/16",8, 0 )
          "10.10.0.0/24"
      > cidrsubnet("10.10.0.0/16",8, 1)
          "10.10.1.0/24"
      > cidrsubnet("10.10.0.0/16",8, 2)
          "10.10.2.0/24"
      > cidrsubnet("10.10.0.0/16",8, 3)
          "10.10.3.0/24"
   -exit-

* inputs.tf
-----------
remove (2) - ex:- "10.10.%g.0/24"


* main.tf (2)
---------
change cidr_block = cidrsubnet(var.vpc_network_cidr,8,count.index)

    ^ terraform fmt
    ^ terraform validate
    ^ terraform apply
  -yes-


--------
## Concepts:-      ----RT(17:00)
* Terraform graph format

    ^ terraform graph
web:- dot format visualizer


-----------
## 06/08/23
------------
## ntier-aws:-

# Creating a Network security group for
----------------------------------------
 * web
    * incoming:
        - http (80): allow to all
        - ssh (22): allow to all

 * app 
    * incoming:
        - ssh (22): allow to all
        - ssh (8080): allow to all

 * db
    * ingress:
        - tcp 3306: allow within vpc range


VSC:-
    {(rename - main.tf to network.tf)]
    ^ git add .
    ^ git commit -m "rename files"
    ^ git pushsub

+ create one file - "securitygroups.tf" ----RT (07:00)
web - aws providers
    aearch - security_group
        --aws security_group--

* securitygroups.tf(1)
--------------------
resource "aws_security_group" "websg" {
  name        = "websg"
  description = "Tis is web security group"
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

["adding additional - "depends_on""]
        --aws security_group--

* Example Usage
Basic usage:-
-------------
# 80 port:-

* securitygroups.tf(2)
-------------------
resource "aws_security_group_rule" "websg_http" {
  security_group_id = aws_security_group.websg.id
  type              = "ingress"       
  from_port         = 80
  to_port           = 80
  protocol          = "tcp"
  cidr_blocks       = ["0.0.0.0/0"]
  depends_on = [
    aws_security_group.websg
  ]
}

# 22 port:-
* securitygroups.tf(3)
-------------------
resource "aws_security_group_rule" "websg_ssh" {
  security_group_id = aws_security_group.websg.id
  type              = "ingress"       
  from_port         = 22
  to_port           = 22
  protocol          = "tcp"
  cidr_blocks       = ["0.0.0.0/0"]
  depends_on = [
    aws_security_group.websg
  ]
}

(NOTE: If want to numbers websg - add "count = 5" in network.tf)

    ^ terraform fmt
    ^ terraform validate
    ^ terraform apply
  -yes-
 -[now added 2 sg]-
Apply complete! Resources: 3 added/ 0 changed, 0 destroyed

* check to aws - what the region and refresh..?
    goto security groups
        selected recent one (websg)
   - inbound rules:-
            seen 2 security groups are added 
    (HTTP:80 / SSH:22) - TCP  - [Source: 0.0.0.0/0]

######
# fainal project
######
* network.tf
------------
resource "aws_vpc" "ntier_vpc" {
  cidr_block = var.vpc_network_cidr

  tags = {
    Name = "ntier"
  }
}

resource "aws_subnet" "subnets" {
  count      = length(var.subnet_cidr_ranges)
  vpc_id     = aws_vpc.ntier_vpc.id
  cidr_block = var.subnet_cidr_ranges[count.index]
  tags = {
    Name = var.subnet_names[count.index]
  }
  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

* security.tf
-------------
resource "aws_security_group" "websg" {
  name        = "websg"
  description = "this is web security group"
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

resource "aws_security_group_rule" "websg_http" {
  security_group_id = aws_security_group.websg.id
  type              = "ingress"
  from_port         = 80
  to_port           = 80
  protocol          = "tcp"
  cidr_blocks       = ["0.0.0.0/0"]
  depends_on = [
    aws_security_group.websg
  ]
}

resource "aws_security_group_rule" "websg_ssh" {
  security_group_id = aws_security_group.websg.id
  type              = "ingress"
  from_port         = 22
  to_port           = 22
  protocol          = "tcp"
  cidr_blocks       = ["0.0.0.0/0"]
  depends_on = [
    aws_security_group.websg
  ]
}
---xx---
--------

 DONE------>>>>------>>>>>>
>.>>.

# What is Inbound rules...?
    - define the traffic allowed to the server on which ports and from which sources.

# What is Outbound rules...?
    - firewall policies that define the traffic allowed to leave your network through secured ports to reach legitimate destinations.

# What is INGRESS RULE...?
    - A rule applies either to inbound traffic (ingress)

# What is EGRESS RULE...?
    - A rule applies either to outbound traffic (egress)


# add onemore resources in securitygroups.tf:-
---------------------------------------------
* securitygroups.tf(4)
-------------------
resource "aws_security_group_rule" "websg_out" {
  security_group_id = aws_security_group.websg.id
  type              = "egress"      -(outbondrule)-
  from_port         = 0             -(minimum)
  to_port           = 65535         -(maximum)
  protocol          = "-1"
  cidr_blocks       = ["0.0.0.0/0"]
  depends_on = [
    aws_security_group.websg
  ]
}

    ^ terraform fmt
    ^ terraform validate
    ^ terraform apply
   -yes-
  --[added outbound ruls]--

* check to aws - what the region and refresh...?
    goto security groups
        selected recent one (websg)
   - outbound rules:-
            seen security groups are added ------RT(22:00)
    (All traffic) - All  - [Source: 0.0.0.0/0]


Done by giving web security groups

---x---



-----------------------------------
[NOTE: iam give inputs by starting]
------------------------------------
* inputs.tf
-----------
variable "vpc_network_cidr" {
  type    = string
  default = "10.10.0.0/16"
  discription = "this is network cidr"
}

variable "subnet_name" {
  type        = list(string)
  default     = ["web1", "web2", "app1", "app2", "db1", "db2"]
  description = "This is subnet names"
}

variable "web_sg_config" {
  type   = object({
    name = string
    description = string
    ruls = list(object({
        type = string
        form_port = number
        to_port = number
        protocol = string
        cidr_block = string
    }))
  })
  default = {
    name = "websg"
    description = "this is websecurity group"
    rules = [ {
        type = "ingress"
        form_port = 80
        to_port = 80
        protocol = "tcp"
        cidr_block = "0.0.0.0/0"
    }]
  }
}

* replace all off the "security.tf" 

* security.tf:- (staring to)      ------------RT(27:05)
resource "aws_security_group" "websg" {
  name        = var.web_sg_config.name     ------->(1)
  description =  var.web_sg_config.description   --->(2)
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

resource "aws_security_group_rule" "websg_rules" {
  security_group_id = "aws_security_group.websg.id"     -->(3) --->RT(29:00)
  count = length(var.web_sg_config.rules)     --->(4)
  type              = var.web_sg_config.rule[count.index].type  --->(5)
  from_port         = var.web_sg_config.rule[count.index].form_port   --->(6)
  to_port           = var.web_sg_config.rule[count.index].to_port     --->(7)
  protocol          = var.web_sg_config.rule[count.index].protocol
  cidr_blocks       = [var.web_sg_config.rule[count.index].cidr_block]
  
    depends_on = [
    aws_security_group.websg
  ]
}


# replace all off the "inputs.tf" ---RT(28:00)
* inputs.tf
-----------
variable "vpc_network_cidr" {
  type    = string
  default = "10.10.0.0/16"
  discription = "this is network cidr"
}

variable "subnet_name" {
  type        = list(string)
  default     = ["web1", "web2", "app1", "app2", "db1", "db2"]
  description = "This is subnet names"
}

variable "web_sg_config" {
  type   = object({
    name = string
    description = string
    ruls = list(object({
        type = string
        form_port = number
        to_port = number
        protocol = string
        cidr_block = string
    }))
  })
  default = {
    name = "websg"
    description = "this is websecurity group"
    rules = [ {
        type = "ingress"
        form_port = 80
        to_port = 80
        protocol = "tcp"
        cidr_block = "0.0.0.0/0"
    },                             --->(0)
    {
        type = "ingress"         --->(1-5) [addining multiple rules]
        form_port = 22
        to_port = 22
        protocol = "tcp"
        cidr_block = "0.0.0.0/0"
    },
    {
        type = "egress"         --->(1-5) [addining multiple rules]
        form_port = 0
        to_port = 65535
        protocol = "-1"
        cidr_block = "0.0.0.0/0"
    }]
  }
}
    --[- iam creating 3-rules -]--

    ^ terraform fmt


+ create a file "dev.tfvars"  (write inputs.tf valus to dev.tfvar) --->RT(31:05)
---------------------------

(NOTE once add valus in dev.tf and remove (defalut valus) in inputs.tf one by one)

# dev.tfvars:-                  -----RT(32:00)
--------------
vpc_network_cidr = "10.10.0.0/16"
subnet_name = ["web1", "web2", "app1", "app2", "db1", "db2"]
web_sg_config = {
    name = "websg"
    description = "this is websecurity group"
    rules = [ {
        type      = "ingress"
        form_port = 80
        to_port   = 80
        protocol  = "tcp"
        cidr_block = "0.0.0.0/0"
    },                             
    {
        type       = "ingress"         
        form_port  = 22
        to_port    = 22
        protocol   = "tcp"
        cidr_block = "0.0.0.0/0"
    },
    {
        type       = "egress"         
        form_port  = 0
        to_port    = 65535
        protocol   = "-1"
        cidr_block = "0.0.0.0/0"
    }]
  }

db_sg_config = {
    name = "dbsg"
    description = "this is dbsecurity group"
    rules = [ {
        type       = "ingress"
        form_port  = 3306
        to_port    = 3306
        protocol   = "tcp"
        cidr_block = "10.10.0.0/16"
    },
    {
        type       = "egress"         
        form_port  = 0
        to_port    = 65535
        protocol   = "-1"
        cidr_block = "0.0.0.0/0"
    }]
  }

app_sg_config = {                   ----RT(43:00)
    name = "appbsg"
    description = "this is appsecurity group"
    rules = [ {
        type       = "ingress"
        form_port  = 8080
        to_port    = 8080
        protocol   = "tcp"
        cidr_block = "10.10.0.0/16"
    },                             
    {
        type       = "ingress"         
        form_port  = 22
        to_port    = 22
        protocol   = "tcp"
        cidr_block = "0.0.0.0/0"
    },
    {
        type       = "egress"         
        form_port  = 0
        to_port    = 65535
        protocol   = "-1"
        cidr_block = "0.0.0.0/0"
    }]
  }


---xx---
---xx---

(NOTE once add valus in dev.tf and remove (defalut valus) in inputs.tf one by one)
{After removing those valus}

fainal inputs.tf are hear:-

# inputs.tf
-----------
variable "vpc_network_cidr" {
  type    = string
  discription = "this is network cidr"
}

variable "subnet_name" {
  type        = list(string)
  description = "This is subnet names"
}

variable "web_sg_config" {
  type   = object({
    name           = string
    description    = string
    ruls    = list(object({
        type       = string
        form_port  = number
        to_port    = number
        protocol   = string
        cidr_block = string
    }))
  })
  description = "This is web security group config"
}

variable "app_sg_config" {      --->(1)
  type   = object({
    name           = string
    description    = string
    ruls    = list(object({
        type       = string
        form_port  = number
        to_port    = number
        protocol   = string
        cidr_block = string
    }))
  })
  description = "This is app security group config" --->(2)
}

variable "db_sg_config" {      --->(3)          RT(33:00)
  type   = object({
    name           = string
    description    = string
    ruls    = list(object({
        type       = string
        form_port  = number
        to_port    = number
        protocol   = string
        cidr_block = string
    }))
  })
  description = "This is db security group config" --->(4)
}

# internals.tf      --->(35:12)
--------------
locals {
    name = "ntier"
}

  ^ terraform fmt

# security.tf:-
--------------
resource "aws_security_group" "websg" {
  name        = var.web_sg_config.name     ------->(1)
  description =  var.web_sg_config.description   --->(2)
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

resource "aws_security_group_rule" "websg_rules" {     -->(3) --->RT(29:00)
  count             = length(var.web_sg_config.rules)     --->(4)
  type              = var.web_sg_config.rule[count.index].type  --->(5)
  from_port         = var.web_sg_config.rule[count.index].form_port   --->(6)
  to_port           = var.web_sg_config.rule[count.index].to_port     --->(7)
  protocol          = var.web_sg_config.rule[count.index].protocol
  cidr_blocks       = [var.web_sg_config.rule[count.index].cidr_block]
  security_group_id = "aws_security_group.websg.id"
  
    depends_on = [
    aws_security_group.websg
  ]
}


resource "aws_security_group" "dbsg" {
  name        = var.db_sg_config.name     ------->(1)
  description =  var.db_sg_config.description   --->(2)
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

resource "aws_security_group_rule" "dbsg_rules" {     -->(3) --->RT(29:00)
    count = length(var.db_sg_config.rules)     --->(4)
  type              = var.db_sg_config.rule[count.index].type  --->(5)
  from_port         = var.db_sg_config.rule[count.index].form_port   --->(6)
  to_port           = var.db_sg_config.rule[count.index].to_port     --->(7)
  protocol          = var.db_sg_config.rule[count.index].protocol
  cidr_blocks       = [var.db_sg_config.rule[count.index].cidr_block]
  security_group_id = "aws_security_group.dbsg.id"
  
    depends_on = [
    aws_security_group.dbsg
  ]
}


resource "aws_security_group" "appsg" {
  name        = var.app_sg_config.name     ------->(1)
  description =  var.app_sg_config.description   --->(2)
  vpc_id      = aws_vpc.ntier_vpc.id

  depends_on = [
    aws_vpc.ntier_vpc
  ]
}

resource "aws_security_group_rule" "appsg_rules" {     -->(3) --->RT(29:00)
    count = length(var.appb_sg_config.rules)     --->(4)
  type              = var.app_sg_config.rule[count.index].type  --->(5)
  from_port         = var.app_sg_config.rule[count.index].form_port   --->(6)
  to_port           = var.app_sg_config.rule[count.index].to_port     --->(7)
  protocol          = var.app_sg_config.rule[count.index].protocol
  cidr_blocks       = [var.app_sg_config.rule[count.index].cidr_block]
  security_group_id = "aws_security_group.appsg.id"
  
    depends_on = [
    aws_security_group.appsg
  ]
}
    ^ terraform fmt

* [iam creating 3 resources groups based on completly dinamic valus]

    ^ terraform apply -var-file="dev.tfvars"
  -yes-

check all the aws - add all the 

    ^ git add . 
    ^ git commit -m "added security groups"
    ^ git pushsub

* refer of sir practice:-
[https://github.com/asquarezone/TerraformZone/commit/723f13d8ce8df16ca05927fba71b44246520c174]

# graphviz online   ----RT(41:35)

    ^ terraform graph
copy the what was you created - 
digraph {

}

web - graphviz online - and paste


# In AWS to make network work       ------RT(44:25)
    - We need to create an internet gateway and attach to vpc
    - We need to add route to the default route table to internet gateway

