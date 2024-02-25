
Create a local repository:-
create one file (gitpractice)
    mkdir gitpractice 
    cd gitpractice
    mkdir day1
    cd day1
    git init 

    git config --global user.name "gtdevops"
    git congig --global user.gmail "gtdevops@gmail.com"
start .

    create one file in your system 'one.txt' and write something

    git status
    git add . (git add one.txt)
    git status
    git commit -m "forst change"
    git status      ------ warking tree is clean
    ----------
   git log (or) git log --oneline
   one commit (head -> mastetr) 

 create another file in pc and write something
        two.txt 
    
    git add .
    git status
    git commit -m "second change"
    git status ---- master is clean
    git log 
 two branchs is crated master always shoe to recent commit 

Head chane
    git checkout (past the commit ID)
now head shows to first commit id
no second commit

    git checkout master
now show to files one.txt and two.txt
    git log 
now move one.txt and two.txt to docs
    git status 
    git add .
    git status 
    gti commit -m "third chage"
     git log
checkout command 

open notepad one,txt (notepad .\docs\one.txt)
change somethig
    notepad .\docs\one.txt
    git status
-------------
day2
-----------
    mkdir day2
    git init
    start .
    mkdir src
    makir test
create new test file
    new-item (new-item ./test/main.py)
    git status 
    git add .
    git log
-----------
    git rm --cached test/main.py
ramove main.py (in staging area)
    git status (add to working tree)

    git commit -m "first"

    new-item 1.txt
    git statrs
    git add .
    git status
git restore --staged 1.txt
    git status
git restore --staged src/main.py
    git status

create 100 files once
    touch {1..100}.txt (this command work only git bash)

delete those 100 files once
    git clean -fd .
    start .

go to day 
    git log
head move to forst commit
    git checkout (commit id)

    touch three.txt
    git status
    git add .
    git commit -m "forth change"
--------------
move to day2
------
    git log
    git branch (apollo)
    git commit -m "second"
    git log --oneline

-------------
day3
------------
    mkdir howgitworks
    cd howgitworks
    git init
    mkdir src test docs
    touch src/main.py
    touch docs/Readme.md
    start .
    git add .
    git commit -m "Added folder structure"
    git log --oneline