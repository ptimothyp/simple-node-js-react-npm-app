# Overview

This file has the command to start the docker containers which are used for the jenkins build pipeline.

## Create the jenkins docker

```cmd 
docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 3000:3000 --publish 2376:2376 docker:dind --storage-driver overlay2
```

## Create the jenkins blueocean custom image

```cmd 
docker run --name jenkins-blueocean --rm --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --publish 8080:8080 --publish 50000:50000 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro --volume c:\Users\Timothy:/home myjenkins-blueocean:1.1 
```

```cmd 
docker stop jenkins-blueocean jenkins-docker 
```

