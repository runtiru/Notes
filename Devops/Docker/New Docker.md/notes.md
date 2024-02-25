## Class 01
------------
Docker play ground 
    login to APS

  * information about container 
    ^ docker container inspect <id of container>
  * list of containers
    ^ docker ps
    ^ docker container ls -a

* delete a single container 
    ^ docker container rm -f <id>

* delete all the container 
    ^  docker container rm -f $(docker container ls -a -q)

* delete all the images
    ^ docker image rm -f $(docker image ls -q)

* know running status of nginx
[docker container run -id --name nginx02 nginx:latest]
    ^ curl http://172.17.0.2

# Port publish of containers:-
* Create on docker container 
  1  ^ docker container run --rm -dit --name ngiex01 --publish 8000:80 nginx:latest

  2  ^ docker container run --rm -dit --name nginx02 --publish 8001:80 sreeharshav/rollingupdate:v1

  3  ^ docker container run --rm -dit --name nginx03 --publish 8005:80 sreeharshav/rollingupdate:v2

know how to run the servers :-
    docker playground   
        open the port id

* goto to container inside
    ^ docker container exec -it <nginx01> bash
[docker container exec -it f49ce3c07e53 bash]

* exit out of the container 
    [contele + pq]

* size of the image (containers)
    ^ docker image ls -a


* how to change nginx sever name 
    - goto instde the container 
    ^ docker container exec -it <nginx01> bash
   * install some nano application 
    ^ apt update && apt install -y nano

    ^ nano /usr/share/nginx/html/index.html
      change name and [ctrl+o, enter, ctrl+x]
relode the web page

{NOTE: DOCKER CONTAINERS ARE BY DEFAULT STATELESS OR EPHERMA}

--------------

## Class 02
-----------
* Create one ec2 loginto docker
    ^ sudo su -
    ^ mkdir build   (create on file )
    ^ nano Dockerfile  (like vi)

Dockerfile:
-----------
FROM (base image)
LABEL (key value)
LABEL (mail)
RUN (create a container)
RUN (update && install)
RUN (unzip)``
