# Docker Commands

## Index
- [General](#general)
  * [Show commands & management commands](#show-commands--management-commands)
  * [Docker version info](#docker-version-info)
  * [Show info](#show-info)
- [General images commands](#general-images-commands)
  * [List images](#list-images)
  * [Pull images](#pull-images)
  * [Remove image](#remove-image)
  * [Remove multiples images](#remove-multiples-images)
  * [Remove all images](#remove-all-images)
- [Containers](#containers)
  * [Run Comand](#run-comand)
    + [Create and run a container in foreground](#create-and-run-a-container-in-foreground)
    + [Create, run and name a container in foreground](#create--run-and-name-a-container-in-foreground)
    + [Create and run a container in background](#create-and-run-a-container-in-background)
    + [Create and run a container in background with a port mapping](#create-and-run-a-container-in-background-with-a-port-mapping)
    + [Create and run a container with specific enviroment variable](#create-and-run-a-container-with-specific-enviroment-variable)
    + [Create and run a container with specific volume assignment](#create-and-run-a-container-with-specific-volume-assignment)
  * [List containers](#list-containers)
    + [Running containers](#running-containers)
    + [All containers](#all-containers)
  * [Container info](#container-info)
    + [All info](#all-info)
    + [Specific property (--format)](#specific-property----format-)
  * [Start existing container](#start-existing-container)
  * [Stop container](#stop-container)
  * [Stop multiples container](#stop-multiples-container)
  * [Stop all running containers](#stop-all-running-containers)
  * [Remove container](#remove-container)
  * [Remove a running container](#remove-a-running-container)
  * [Remove multiple containers](#remove-multiple-containers)
  * [Remove all containers](#remove-all-containers)
  * [Run command in a container](#run-command-in-a-container)
  * [Go into the container](#go-into-the-container)
  * [List processes running in container](#list-processes-running-in-container)
  * [Get logs](#get-logs)
  * [Performance stats (cpu, mem, network, disk, etc)](#performance-stats--cpu--mem--network--disk--etc-)
  * [Examples](#examples)
- [Images Creating](#images-creating)
  * [Dockerfile Parts](#dockerfile-parts)
  * [Build Image](#build-image)
- [Docker Compose](#docker-compose)
  * [Sample compose file (From Bret Fishers course)](#sample-compose-file--from-bret-fishers-course-)
  * [To run](#to-run)
  * [To run in background](#to-run-in-background)
  * [To cleanup](#to-cleanup)
- [Networking](#networking)
  * [Get container port mapping](#get-container-port-mapping)
  * [List networks](#list-networks)
  * [Inspect network](#inspect-network)
  * [Create network](#create-network)
  * [Create container on network](#create-container-on-network)
  * [Connect existing container to network](#connect-existing-container-to-network)
  * [Disconnect container from network](#disconnect-container-from-network)
  * [Detach network from container](#detach-network-from-container)
- [Image Tagging & Pushing To Dockerhub](#image-tagging---pushing-to-dockerhub)
  * [Retag existing image](#retag-existing-image)
  * [Upload to dockerhub](#upload-to-dockerhub)
  * [Docker Login](#docker-login)

## General

### Show commands & management commands

```bash
docker
```

### Docker version info

```bash
docker version
```

### Show info

The command shows info like number of containers, etc.

```bash
docker info
```

## General images commands

### List images

The command lists the images we have pulled.

```bash
docker images
```

### Pull images

To pull down images:

```bash
docker pull <image:tag>
```

### Remove image

```bash
docker image rm <image_name or id>
```

or

```bash
docker rmi <image_name or id>
```

### Remove multiples images

```bash
docker rmi <image_name_1 or id_1> <image_name_2 or id_2> <image_name_n or id_n>
```

### Remove all images

```bash
$ docker rmi $(docker images -a -q)
```
>-a, --all   Show all images

>-q, --quiet Only show image IDs


## Containers

### Run Comand

#### Create and run a container in foreground

```bash
docker container run <image_name:tag>
```

#### Create, run and name a container in foreground
```bash
docker run --name <container_name> <image:tag>
```

#### Create and run a container in background

```bash
docker container run -d <image:tag>
```
It is possible to attach the container with the command:

```bash
docker attach <container_name or id>
```


#### Create and run a container in background with a port mapping

```bash
docker container run -d -p <host_port>:<container_port> <image:tag>
```

#### Create and run a container with specific enviroment variable

```bash
docker run -e <ENVIROMENT_VARIABLE_NAME=value> <image_name>
```

#### Create and run a container with specific volume assignment

```bash
docker run -v <host_volume:path_to_mount> <image_name>
```

### List containers

#### Running containers

```bash
docker container ls
```

or

```bash
docker ps
```

#### All containers 

```bash
docker container ls -a
```

OR

```bash
docker ps -a
```

### Container info

#### All info

```bash
docker container inspect <container_name or id>
```

#### Specific property (--format)

```bash
docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <container_name or id>
```

### Start existing container

```bash
docker container start <container_name or id>
```

### Stop container

```bash
docker container stop <container_name or id> 
```

### Stop multiples container

```bash
docker container stop <container_name_1 or id_1> <container_name_2 or id_2> <container_name_n or id_n>  
```

### Stop all running containers

```bash
docker stop $(docker ps -aq)
```
>-a, --all   Show all images

>-q, --quiet Only show image IDs

### Remove container

With the next command is not possible remove running containers, must stop first.

```bash
docker container rm <container_name or id>
```

### Remove a running container

```bash
docker container rm -f <container_name or id>
```

> -f, --force     Force the removal of a running container (uses SIGKILL)

### Remove multiple containers

```bash
docker container rm <container_name_1 or id_1> <container_name_2 or id_2> <container_name_n or id_n>
```

### Remove all containers

```bash
docker rm $(docker ps -aq)
```

>-a, --all   Show all images

>-q, --quiet Only show image IDs


### Run command in a container

```bash
docker exec <container_name or id> <command>
```

### Go into the container

```bash
docker exec -it <container_name or id> bash
```

### List processes running in container

```bash
docker container top <container_name or id>
```

### Get logs

```bash
docker container logs <container_name or id>
```

### Performance stats (cpu, mem, network, disk, etc)

```bash
docker container stats <container_name or id>
```

### Examples

**NGINX**

```bash
docker container run -d -p 80:80 --name nginx nginx (-p 80:80 is optional as it runs on 80 by default)
```

**APACHE**

```bash
docker container run -d -p 8080:80 --name apache httpd
```

**MONGODB**

```bash
docker container run -d -p 27017:27017 --name mongo mongo
```

**MYSQL**

```bash
docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql
```


## Images Creating

### Dockerfile Parts

- FROM - The OS used. Common is alpine, debian, ubuntu.
- ENV - Environment variables.
- RUN - Run commands/shell scripts, etc.
- COPY - Copies files from host to container.
- EXPOSE - Ports to expose.
- WORKDIR - Sets working directory (also could use 'RUN cd /some/path').
- CMD - Sets default parameters that can be overridden from the Docker Command Line Interface (CLI) when a container is running.
- ENTRYPOINT - Default parameters that cannot be overridden when Docker Containers run with CLI parameters.

### Build Image

```bash
docker build -f <docker_file> -t <app_name:tag> <path>
```


## Docker Compose

- Configure relationships between containers
- Save our docker container run settings in easy to read file
- 2 Parts: YAML File (docker.compose.yml) + CLI tool (docker-compose)

### Sample compose file (From Bret Fishers course)

```apache
version: '<version>'

# same as
# docker run -p <host_port:container_port> -v <host_volume:path_to_mount> <image_name>

services:
  <service_name>:
    image: <image_name>
    volumes:
      - <host_volume:path_to_mount>
    ports:
      - <host_port:container_port>
```

### To run

```bash
docker-compose up
```

### To run in background

```bash
docker-compose up -d
```

### To cleanup

```bash
docker-compose down
```


## Networking

### Get container port mapping

```bash
docker container port <container_name or id>
```

### List networks

```bash
docker network ls
```

### Inspect network

```bash
docker network inspect <network_name>
```

### Create network

```bash
docker network create --driver <driver(default=bridge)> --subnet <subnet> --gateway <gateway> <network_name>
```

### Create container on network

```bash
docker container run -d --name <container_name> --network <network_name> <image>
```

### Connect existing container to network

```bash
docker network connect <network_name> <container_name>
```

### Disconnect container from network

```bash
docker network disconnect <network_name> <container_name>
```

### Detach network from container

```bash
docker network disconnect
```


## Image Tagging & Pushing To Dockerhub

### Retag existing image

```bash
docker image tag <existing_image_name> <new_repository/new_image_name:new_tag>
```

### Upload to dockerhub

```bash
$ docker image push <new_repository/new_image_name:new_tag>
```

### Docker Login

```bash
docker login
```