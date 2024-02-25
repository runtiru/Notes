Shell Script:

#!/bin/bash

    ^ sudo vi c_d.sh
write some commands 
```bash
#!/bin/bash

# create a directory
sudo mkdir Ram
```
exit
now run the script
    ^ sh c_d.sh
now create `Ram` folder 
    ^ ls
`Ram`
=============================================
    ^ sudo vi c_v.sh
```bash
#!/bin/bash

echo "started removing forlder new folder"
sudo rm -rf Ram 

echo "started creating files and folder"
sudo mkdir Ram 

# Permissions 
sudo chmod 666 Ram

```
==============================================
    ^ sudo vi c_v.sh
```bash
#!/bin/bash
# string 
echo "key = value (string)"

name="RAM"

echo "my name is $tiru"

age=25
networkip=10.1.0.0/16
village="hsl"
echo "{name : $name, age: %age, location: %village , networkip: %networkip}
```
==============================================

Eg:-
= (equal)
!= (notequal)
<= (gaterthanequl)
>= (lessthanequal)
< 
>

A=5
B=4

if [A<=B] than
echo "A is greather than B"
if 

if [A<=B] than 
echo "B is higer valure than A"
elif "B is "

==============================================

### Environmental Variables
ENV:-

Eg:-
```bash
#!/bin/bash
teat () {
echo "$1 $2 $3"
}

test "t1", "t2", "t3"
```
-------------

    ^ sudo vi if.sh 
```bash
#!/bin/bash
name="Ram"

date() {
    echo "{name: $1, age: $2, location: $3}"
}

data "Ram", "22", "Vizag"
```
---------------

    ^ sudo vi sample.sh
```bash
#!/bin/bash

echo "started function"

sudo chmod 777 if.sh
sh if.sh "Ram", "22", "vizag"
```

---------------

    ^ sudo vi /etc/environmrnt
```bash
#!/bin/bash
# add something what you need

```
now add the source
    ^ source /


## Loop

    vi loop.sh
```bash

```