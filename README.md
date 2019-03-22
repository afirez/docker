# ENV
- Vagrant ( Optional )
- VirtralBox ( Optional )
- Box envimation/ubuntu-xenial-docker ( Optional )
- Docker ( Needed )

# CHANGELOG

## android-jenkins


```
$ cd android-jenkins
$ sudo docker build -t afirezd/jenkins:1.0.0 .
$ docker run -d -p 8080:8080 afirezd/jenkins:1.0.0
$ docker run ps 
$ sudo docker exec ${container_id} cat /var/jenkins_home/secrets/initialAdminPassword
$ docker exec -it ${container_id} /bin/bash

```

## androidbuilder

```

$ cd androidbuilder
$ sudo docker build -t afirezd/androidbuilder:v1.0.0 .


```
