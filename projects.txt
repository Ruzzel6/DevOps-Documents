curl -fsSL  https://raw.githubusercontent.com/ajiahamed/deployment/refs/heads/main/docker.sh | bash


> sudo usermod -aG docker <username>   //To give sudo privilege to user
> docker ps -a   //Stopped containers
> docker run -d --name my-apache -p 8080:80 httpd
> docker stop CntID
> docker restart cntid
> docker rm CntID
> docker rmi imagename

> docker container prune   //removes all stopped containers
> docker prune images      //removes unused/untaged images 
> docker image prune -a   //To remove all images not used

1)Creating Dockerfile >> building image >> running app
> docker build -t hello-app .
> docker run -d --name python-application hello-app
> docker run -it --name python-app2 hello-app


> docker exec -it containerID sh   //interactive
> docker logs 0aad4c46960c        //To find logs  
>  docker run --name helocmd2 hello "ls"  //Passing command to cmd
> docker run --name check24dedr hello sh -c "cd bin && ls"   //Run two commands 

> docker inspect contID
> docker logs

> docker volume ls
> docker volume create Volumename
> docker volume inspect vulumename
> docker volume rm volumename
> docker run -d -v my_volume:/app/data busybox  //To attach volume /app/data is the workdir 
						//stored in /var/lib/docker/volumes/	
============================================================================
Docker Swarm:

> Install docker in all 3 nodes: 
> https://docs.docker.com/engine/swarm/swarm-tutorial/
 
# docker info     //to check 
# docker node ls  //To check nodes in master server

# docker service create --name web --replicas 3 -p 80:80 nginx
# docker sercvice ps web  //To check the where teh containers created

To check: 
# docker service create --name web --replicas 3 -p 80:80 nginx
# sudo docker service scale web=5
# docker service update --image nginx:1.25 web   //To do a rolling update

# docker node promote yr4q0mk0h5xwmfrzos924dhp0
Node yr4q0mk0h5xwmfrzos924dhp0 promoted to a manager in the swarm.

# sudo docker node demote yr4q0mk0h5xwmfrzos924dhp0
Manager yr4q0mk0h5xwmfrzos924dhp0 demoted in the swarm.


==================================================================================================
1) Dockerfile Apache in ubuntu
==========================
# Use Ubuntu as the base image
FROM ubuntu:20.04
 
# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive
 
# Update and install Apache
RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean
 
# Copy custom web content (optional)
COPY index.html /var/www/html/index.html
 
# Expose port 80 for Apache
EXPOSE 80
 
# Start Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
==========================================

2)Python app.
===============
Print hello world
 
# Use Ubuntu as the base image
FROM ubuntu:latest
 
# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive
 
#Wordirectory
WORKDIR /app
 
COPY . /app
 
RUN apt-get update && apt-get install -y python3.8 python3-pip
 
CMD [ "python3", "hello.py"]
===============

3)Flask app
===============
FROM ubuntu:20.04
WORKDIR /opt
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip3 install flask
COPY app.py /opt/
EXPOSE 5000
CMD ["python3" , "app.py"]
===============

4) Yarn app
=======================
FROM node:18.0.0-alpine
 
WORKDIR /app
 
COPY . /app
 
RUN yarn install
 
EXPOSE 3000
 
CMD ["node" , "src/index.js"]
=========================

5) NPM app: (node app)
===============
FROM node:18.0.0-alpine
 
WORKDIR /app
 
COPY . /app
 
RUN npm install
 
EXPOSE 3000
 
CMD ["node" , "index.js"]
-----------------------------------------------------------------------------------------

Java application:
===================
 (A .class file is a file This process converts the human-readable Java source code into bytecode that the Java Virtual Machine (JVM) can understand and execute.}
=================

# Use openjdk base image
FROM openjdk:26-slim-bullseye

# Set working directory
WORKDIR /app

# Copy Java source code into container
COPY hello.java .

# Compile the Java source code To make .class file
RUN javac hello.java


# Set the command to run the compiled Java program
CMD ["java", "hello"]
~                         

>> docker build -t javahello.app .
>> docker run --name javahelloworld javahello.app

---------------------------------------------------------------------------

DOCKER CPOMPOSE:
====================

# cat docker-compose.yaml
version: "3.8"
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app


+++++++++++++++++++++++++++++++++++++++
Node app and MongoDB

# cat docker-compose.yml

version: "3"
services:
  nodeapp:
    build: ./app
    ports:
      - "3000:3000"
    environment:
      - MONGO_URL=mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  mongo:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:




