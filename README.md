# Demo project to deploy a basic python project with docker-compose

docker and docker-compose are extremely useful when -
1. you have a single devlopment machine and you are working on multiple projects and these projects' environment needs to be isolated so that you don't keep on solving python package or system package dependencies 

[Ref: https://docs.docker.com/compose/gettingstarted/]


Here we have a Simple python project with multiple library dependencies defined in the requirements.txt

# Steps to build and deploy the project

## Step 1
We create a DockerFile that help us build a docker image, that will have the required python environment and other dependencies.

## Step 2
We create a docker-compose.yaml file as our project depends on other services as well.  
Generally, if you need to perform multiple steps in order to process(build/compile) and start required services (e.g database, middleware etc) 
you can define them in a Compose file. 
In our example,  [docker-compose.yaml](docker-compose.yaml) file defines two services: 
1. web 
2. redis

The `web` service uses an image that is built with the [Dockerfile](Dockerfile) in the current directory. It then binds the container and the host machine to the exposed port, 8000. This example service uses the default port for the Flask web server, 5000.

The `redis` service uses a public Redis image pulled from the [Docker Hub registry](https://hub.docker.com/) .

To build and deploy the app you can use following command
```
docker-compose up
```

If you face permission errors while running the docker or docker-compose, you need to create the user group `docker` with required permisions as following
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
Now you can run docker-compose as 
```
newgrp docker
docker-compose up

```

You can visit http://172.20.0.3:5000/ to see the hit count