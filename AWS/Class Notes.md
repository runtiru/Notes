Cinsole:-
        aws console
    (web server + AWS)
Programmatic
        bash / powershell
    
Activce directory:-

### 26/07/32
-------------
### AWS User Management Concepts
Organizatins (so may accounts)
        AWM IAM (identity access managment) Concepts:
                User: indivisual 
                Group:minimize your work
                Role: Permision to one AWS service for access on other AWS services.
                Policy: 

Scenarios:-
------------
       * recreate users
       * Sync/Federate uersr
* Permission managment
* Mulitple Accounts i.e Organizations
* * * * 
Try to do note what doing your IT friend in daily work
-------------------------
# 28/07/23
-------------------------
### JSON :- 
     JavaScript Object Notation :- the data-exchange format that makes this possible
        represent ot NAME, VALUE PAIRS
        

-------------------------
# 28/07/23
-------------------------
### Identity and access management (contd...)
        * IAM Policy Grammar
                        (Grammar or syntax)

* 3 eliments of IAM Policy
        1. Version block
                A. New version
                B. Old version
        2. ID block
        3. Statement block (arre of statment)
                 each statment combinatios of 
                        * principal block - which user
                        * effect block - allow/deny
                        * action block - what aew the actions
                        * resource block - on which resoure
                        * condition clock -

  ( * repersent - anything / all the actions / full access )
        Ex:- "ec2:*" ( it means allow all the ec2 permitions )

Ex:-
    ec2 => 250 actions 
        allow => "ec2: *" => show all 250 actions
        deny => "ec2:Terminate: *" => 

( * - all access )
Get* - all the access of get
List* - all the access of list
        Ex:- s3:Get* ---> all get access of s3
             s3:List* ----> all list access of s3

## create own policy and give permistons of s3, ec2 
----------------------------------------------------
    

------------
### 03/08/23
------------
lanch 2 Ec2 instancs (micro)
        1.should start
        2. should not start

ARN for EC2:-  (Amazon Resource Name)
--------------------------------------



----------------------
## 08/08/23 & 09/08/23
-----------------------
# Cloud formation
 create a vpc in aws (manaul)

* setup VSC
        
------
## 13/08/23

# change 9: Create a web VM
* Make the following a parameter
        * ami ID
 (reffer to class room notes)

# change 10: Create a databash

        - need 2 differnt zones
    what is - string
            - blooin
            -
            
-----------
## 16/08/23
-----------
### ntier arcti 

* create a cloudformation template to create a security group
      Create a folder "securitygroup"
        inside "main.json"
    web - aws clioudformation tags
        json
          ....
          ....
          ....
          ....
          ....
* main.json
------------


======================================================
## 18/08/23
-----------
### Storage in an enterprise and needs in cloud
-----------------------------------------------

* Hardware type (storage)
     - Hard Disk (HD)
     - Network disk storage
     - Blob storage
        - Format....?

* Storage Needs by usecase
    - Sever/Laptop OS
    - Shared Storage (files storage)
    - Databases:- storage the data
        * Data
           - Business Intelligence
           - Analytics
           - Prediction
    - Data Lakes
    - Archival

# Terms
-------
* Backup - 
* Archivai - to recover form digesters

* Differnce between 
        - kb and KIB
        - GB and GiB
        - TB and TiB

* Units for performance for storage
    - IOPS (inputs/outputs )

* Durability:- the ability to last over time, resisting wear, breakage, deterioration, etc


* what is cloud infrastructure...?
* what is aws do...?

-----------
## 19/08/23
-----------
### AWS Global Infrasture
-------------------------
* Typical Datacenters:


* Latency:- the travel time of two systerms


# 

* S3 :- Blob storage
                - add any file or uplode any file 
* Glacier:- Archival storage

* EFS(Elastic File System): Network drive

* FsX(file systems and backups): Network drives for
        - Windows
        - Other third parties like netapp
        
* EBS(Elastic Block Store): 

## 22/08/23
------------
### AWS Storage
----------------
* Blob storage or Object storage:-
       - this is a storage system for files.
       - a type of cloud storage for unstructured data. 


# 23/0823
---------
## Find destinations in S3 URI formats
---------------------------------------
* S3 URI Format:-
        * Bucket: `s3://<bucket-name>`
        * Folder: `s3://<bucket-name>/<folder-name>`
        * Object: `s3://<bucket-name>/<objrct-name>` (or)

`s3://<bucket-name>/<folder-name>/<folder-name>`


## Storage classes in S3
-------------------------
* Create an s3 bucket and upload some object



arn:aws:s3:::runmys3buck

----------
# 24/08/23
----------
### AWS Global Network
----------------------
     - a single, private network that acts as the high-level continers for your network objects.


## 31/08/23
-----------
## Latency
    - 



## 16/09/23
------------
### AWS RDS
-----------
# how to make Database Highly Available
* Scale 
* Replication 

  M (Master) - Read/Write
  R (Replica) - only one permition like R or W
  S (Standby) - once die master standby was replace the master place (standby become a master)
  Multi-AZ - Both master and Standby

* Read-Repllica
     - Report - read the date but not change the data
* Read/Write-Replica
   - endpoint :

* Additional datbases inthe same region but differcen AZ, use multi-AZ
   * Promotion

# Create read replica (differnt region)
---------------------------------------
  - 
# Create Multi-AZ (sS)

=> Severless


## 26/09/23
-----------
### AWS CLI
   Activity2: Create a mysql rds instance
        Steps:
                Create a subnet group
                Create a securiry group
                Create a rds instance

## 27/09/23
-----------
   ^ bash -x
   ^ bash -x ./

===============================================
## 04/10/23
#### Migration
---------------
# Compute Services in AWS
* EC2:-
    - Auto scaling groups
    - Serverless 
* clud attem fram work
* Landing zone
* Migration Phaese
     - Discover
     - Assess
     - Plan
     - Migrate
     - Modernize

### Storage Migration 
----------------------
