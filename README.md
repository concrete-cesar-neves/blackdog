# Learn The Basics About Docker

This documents provides a Docker start-guide for beginners.

## Table of Contents :scream:

* Installing Docker
* Create a Docker Image using Debian running a Hello World website
* Create an account on DockerHub and upload your image
* Use 2 images available on DockerHub to set up an application

## Pre requisites

* Docker 1.7+ **
* Mac OS Sierra **


### Installing Docker on Mac OS 

Download Docker Community Edition on [Docker website](https://www.docker.com/community-edition)
1. Just install the Docker.dmg downloaded
2.  Access your terminal and check the installation with the command: 

    docker version

## Create a Docker Image using Debian running a Hello World website

### Download Debian image to your docker images

On terminal of your local system:

    docker pull debian

### Running a container with your new Docker Image

On terminal of your local system:

    docker run -it -p 8282:80 debian /bin/bash

** note: **

>  8282:80 means that the port 8282 on your local system will run the port 80 from your  container.

### Installing apache on your Debian container

On terminal of your container running Debian:

    apt-get update

	apt-get install apache2

	echo "Hello World ;)" > /var/www/html/index.html

	/etc/init.d/apache2 start

On your local system:

> just access your local Web Browser and hit the url: http://localhost:8282


## Create an account on DockerHub and upload your image :cloud:

Acess the [DockerHub website](https://hub.docker.com) to create your account


### create your custom Debian Image

On terminal of your local system:

    docker commit <containerID> <name_of_your_custom_image_only_lower_case>.

	Example: docker commit 8377f56db064 test/debian-apache


### Upload your imagem to DockerHub

On terminal of your local system:

    docker login (login with your DockerHub login/password)

		docker tag <your_image_name> <your_login_on_dockerhub> <name_your_image_on_github>

		Example: docker tag cesar/debian-apache cesarneves/debian-apache

		docker push <name_of_your_image>

		Example: docker push debian-apache


#### Creator

	César Neves

