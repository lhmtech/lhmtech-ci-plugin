Setup jenkins server with docker
================================

## Install docker
refer the [Ubuntu Development Environment Setup](https://bitbucket.org/healthsource/healthsource/wiki/Ubuntu_Dev_Env_Setup)

## Pull docker image
```
docker pull jenkins
```

## Run jenkins docker container
Prepare local volume /home/lihe/jenkins_data, then
```
docker run -p 8080:8080 -p 5000:5000 -v /home/lihe/jenkins_data:/var/jenkins_home --name jenkins-ci -d jenkins
```
Some tips:

* To start docker container
```
docker start jenkins-ci
```

* To stop docker container
```
docker stop jenkins-ci
```

* Attach to container with bash interactively
```
docker exec -i -t jenkins-ci bash
``` 

## Using systemd to start/stop container with Linux
```
cd /etc/init
sudo nano jenkins-ci.conf
```
Put the following:
```
description "jenkin-ci daemon"

start on filesystem and started docker
stop on runlevel [!2345]

respawn

script
        /usr/bin/docker start -a jenkins-ci
end script
```