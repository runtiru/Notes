Git:-
    Is a DevOps tool used for source code management.
     :-is a version control system (VCS) used for tracking changes in computer files.
     :- It is generally used for source code management in software development.
     :-Git is used to tracking changes in the source code
          - The distributed version control tool is used for source code management
          - It allows multiple developers to work together
          - It supports non-linear development through its thousands of parallel branches

    Features of Git
          Tracks history
          Free and open source
          Supports non-linear development
          Creates backups
          Scalable
          Supports collaboration
          Branching is easier
          Distributed development

     In Git we have 5 areas
          1. Working tree/directory
          2. Staging area/Cache area
          3. Local repository
          4. Remote Repository
          5. Stash

     APS
    power shell:- 

Local repository :-
## Git:-
---------
open choco and serach the git (how to install git on choco)

copy git installation id on  choco web

coming to - APS
past the id on aps
now install and run the git..........

mkdir (some name - like gitpractice)
now create a flower the same name (gitpractice)...

and create a new directry 
mkdir (some name - day1)
start . (give this command)

now we can seen visvally also
goto ( C drive - users - balu - some name(gitpractice first creating name) - second some (day1) - inside some  .git folder create autometically )

(git init ) 

hedden iteams hear ( goto view and sellect the hidden iteams and file name extensions)
--------------------------------------------
--------------------------------------------
PS C:\temp\gitpractice\day1> (shoing like )
command       git config --global user.name "qtkhahadevops" enter
PS C:\temp\gitpractice\day1> 
command       git config --global user.email "tirumalag@gmail.com" enter
-------------------------------------------
---------------------------------------
goto day one floder create new some test file (like one.txt) inside the one.txt (hello text)
--------------------
coming to PS
ls
git status  (this com know how many files in )
red colour - still in working tree
green colour - movie to staging area
------------------------------------------------------
how to change staging area..........?
git add one.txt
git status 

(now seen the colour of green )
one.txt movie in working tree to staging area
-----------------------------------------------------
create a commit .............?
git commit -m "first change"
git status
(now we can see what are the changes)
----------------------------------------------------
for every commit git gives commit is with username, email, message and date time information..............?
git log (command)

----------------------------------------------------
create a new file and change the content of 'one.txt'........?
git status
(one file - modified and another one untracked fill)
25

------xxxx---------
------xxxx---------


### Administrator windows powersherr
ssh-keygen (3ent)
---
cat ~/.ssh/id_rsa.pub (public key) - 
cat ~/.ssh/id_rsa (private key) - 
----
start . (see the file where the store - .ssh)
copy id.rsa(P) - ( file with note pad )
-----
aws
open - key pairs - goto (Actions) and inport key pair (do the instructions and create a key)
----------
goto instances - launch instances - 
give a neme
select ubuntu
AMI (free tier eligible)
Instance type (free tier eligible)
Add a key pair
network ssettings [ 1- default, 2- subnet (us-east-1a), 3- enable, 
------------
firewall -[(1 security group, 2 name (ssh), 3 description (this will be open ssh from anywhere)
(((( (select existing security froup - select default))))                     launch instance......

goto instance
selete witch instance you five after running the server
copy the public IPv address
------------
(((((security instances)))))))
-------------
open power shell 
give a command - ssh ubuntu@(copy link )
yes
------------
-------------
----------------
day (3)........
-----------
once run ubuntub 
sudo apt update
sudo apt install nginx -y
----------
open instance and copy the public key and past a new window - past the public key 
-----------
now continew the ngnex ..................

l
-------------
aws
### Red hat
------------
past ps 
ssh -i "ramkey.pem" ec2-user@ec2-54-234-148-249.compute-1.amazonaws.com

sudo dnf install httpd

sudo systemctl start httpd

sudo dnf install php -y

sudo systemctl start httpd

sudo systemctl enable httpd


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
            - any change on the masterbranch means that giving relese your coustmer (or) clint
            - no developer will directly can submit the changes on masterbranch
            - masterbranch is rouldout
        - its create
          develop branch
            - any commit that are develop in develop
            branch represent that is done on developer


    2. Develop Branch  
            - its represent by individual developers
            - developers dont directly work on master branch
            - only do marge changes
        - its create
           feature/task branch (its not a part of git, its developer local laptops)
            - push the changes into feature branch


    3. Feature Branch/ Task Branch (Developers)
            - developr make the commits hear
    'developers changes the whant clint required'
            - once done the changes developer will 'marge' to develop branch

--------------> (Day Build)
    
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

# Git lab branching strategies:-----RT(18:25)

- your branch represtnt your environment

    *. Master 
        - Deployed on staging (staging environment)
        - deploy to pre-production
        - 
    *. Pre-Production
        - deploy to production
        - 
    *. Production
## refer to:- https://coderefinery.github.io/git-intro/basics/ 

## Pull-requsts -----RT(25:00)
---------------
    - it is a future of git repository
    
GitHub.com
    (Install)

    create a fork