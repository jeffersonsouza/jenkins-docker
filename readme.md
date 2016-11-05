# Jenkins 2 with Docker
Jenkins 2 inside docker containers using containers as slaves to build PHP and NodeJS

To run this project, just clone, and run the docker compose file. It will start the Jenkins Master with useful plugins and PHP 5.6, PHP 7 and NodeJS 4 slaves.

To start via docker compose just run the follow:

``` yaml
version: '2'
services:
    jenkins:
        image: jeffersonsouza/jenkins:alpine
        privileged: true
        restart: always
        ports:
            - "8085:8080"
            - "50000:50000"
        volumes:
            - jenkins-data:/var/jenkins_home/
            - /var/run/docker.sock:/var/run/docker.sock
    node:
        image: jeffersonsouza/jenkins:slave-node
        privileged: true
        ports:
            - 22
        volumes:
            - jenkins-data:/var/jenkins_home/
            - /var/run/docker.sock:/var/run/docker.sock
    php:
        image: jeffersonsouza/jenkins:slave-php
        privileged: true
        ports:
            - 22
        volumes:
            - jenkins-data:/var/jenkins_home/
            - /var/run/docker.sock:/var/run/docker.sock
    php56:
        image: jeffersonsouza/jenkins:slave-php5
        privileged: true
        ports:
            - 22
        volumes:
            - jenkins-data:/var/jenkins_home/
            - /var/run/docker.sock:/var/run/docker.sock
volumes:
    jenkins-data:
        driver: local
```
@todo More docs: soon. :)
