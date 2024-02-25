# Introduction of DevOps
------------------------
* SDLC (Software Development Life Cycle):-
    -  a process of planning, creating, testing, and deploying information systems across hardware and software.

* Waterfall Model:-
    - first time to instroduce software model

    Analysis (Requirement)
        Design
            Development 
                Testing
                    Deployment
                        Maintenance

* Agile Model:-
    - Client requirements are better understood because of the cinstant feedback
    - Product delivered much faster as compared to waterfall model.

---

* Plan

* Code - vsc(git)

* Build - maven

* Test - junit, se
                                    ==> CI
* Release (Integrate) - jenkins

* Deploy - ansible, puppet, TOMCAT

* Operate

* Monitoring - splunk, negios 
                                    ==> CD


### Docker
----------
* Docker main components
    - Cgroups (controle groups)
    - Volumes
    - File system


Docker File ---------> Docker Image ----------> Docker Container

    ^ docker build -t myimage dockerfile


