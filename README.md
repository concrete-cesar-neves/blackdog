# Learn The Basics About Docker

This documents provides a Docker start-guide for beginners using __Mac OS High Sierra.__


![DockerLogo](/images/dockerLogo.png)


## Table of Contents

* Installing Docker
* Create a Docker Image using Debian running a Hello World website
* Create an account on DockerHub and upload your image
* Use 2 images available on DockerHub to set up an application

## Pre requisites

* Docker 1.7+ 
* Mac OS High Sierra 



### Installing Docker

Download __Docker Community Edition__ on [Docker website](https://www.docker.com/community-edition)
1. Just install the __Docker.dmg__ downloaded
2. Access your terminal and check the installation with the command: 

    docker version

## Create a Docker Image using Debian running a Hello World website

### Download Debian image to your docker images

On your local system:

    docker pull debian

### Running a container with your new Docker Image

On your local system:

    docker run -it -p 8282:80 debian /bin/bash

__note:__

>  8282:80 means that the port 8282 on your local system will run the port 80 from your  container.

### Installing apache on your Debian container

On your container running Debian:

    apt-get update

	apt-get install apache2

	echo "Hello World ;)" > /var/www/html/index.html

	/etc/init.d/apache2 start

On your local system:

> just access your local Web Browser and hit the url: http://localhost:8282


## Create an account on DockerHub and upload your image

Acess the [DockerHub website](https://hub.docker.com) to create your account


### create your custom Debian Image

On your local system:

    docker commit <containerID> <name_of_your_custom_image_only_lower_case>.

	Example: docker commit 8377f56db064 test/debian-apache


### Upload your imagem to DockerHub

On your local system:

    docker login (login with your DockerHub login/password)

		docker tag <your_image_name> <your_login_on_dockerhub> <name_your_image_on_github>

		Example: docker tag cesar/debian-apache cesarneves/debian-apache

		docker push <name_of_your_image>

		Example: docker push debian-apache


## Use 2 images available on DockerHub to set up an application

To conclude this task we`ll use an image of __WordPress__ and another of __MySQL.__ 
First we need to create a directory on our local system to mantain the data base files:

    mkdir -p /docker/myapp/db_volume

Next we need to create inside the directory __/docker/myapp__ a file named __docker-compose.yml__

Edit the file and put into it the following code:


    version: '3'

    services:
    db-wordpress:
     image: mysql:5.7
     volumes:
       - ./db_volume:/var/lib/mysql
     ports:
            - "32779:3306"
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress
     networks:
            - net-app

     wordpress:
      depends_on:
        - db-wordpress
      image: wordpress:latest
      ports:
        - "8181:80"
      restart: always
      environment:
        WORDPRESS_DB_HOST: db-wordpress:3306
        WORDPRESS_DB_USER: wordpress
        WORDPRESS_DB_PASSWORD: wordpress
       networks:
            - net-app
     volumes:
      db_volume:
     networks:
      net-app:
         driver: bridge



### Running your docker-compose

The __docker-compose.yml__ contain information that Docker consume to automate the proccess of create an app environment running two containers: 

* wordpres with a Web Server
* MySQL to matain databases files of your WordPress Blog

On your local system:

    cd /docker/myapp/
    docker-compose up -d



Wait until the script terminates. As soon as the Docker conclude the installation of the images, run the following command to confirm that the new containers was created 


On your local system:

    docker ps


Probaly you will see the containers:

* wordpress:latest
* mysql:5.7


### Accessing your WordPress Blog

Open a Web Browser on your local system and hit the url: http://localhost:8181

You will see the wodpress install screen



#### END :metal:




#### Creator

	César Neves

