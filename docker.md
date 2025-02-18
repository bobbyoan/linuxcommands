---
title: docker
description: 
published: true
date: 2025-02-18T09:28:16.700Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:14.335Z
---

# Docker Commands

## Basics

```bash
docker --version - show docker version
docker info - display system information
```

## Images

```bash
docker images - list all images
docker pull [image] - download an image
docker build -t [name] - build an image from dockerfile
docker rmi [image] - remove an image
docker tag [image] [new_image] - tag an image
```

## Containers

```bash
docker ps - list running containers
docker ps -a - list all containers
docker run [image] - run a container from an image
docker run -it [image] - run a container in interactive mode
docker run -d [image] - run a container in detached mode
docker stop [container] - stop a running container
docker start [container] - start a stopped container
docker restart [container] - restart a running container
docker rm [container] - removes a container
docker exec -it [container] [command] - execute a command inside a running container
```

## Networks

```bash
docker network ls - list all networks
docker network create [name] - create a new network
docker network rm [name] - remove a network
docker network inspect [name] - inspect a network
docker run --network [network] [image] - run a container on a specific network
```

## Volumes

```bash
docker volume ls - list all volumes
docker volume create [name] - create a new volume
docker volume rm [name] - remove a volume
docker run -v [volume]:[path] [image] - run a container with a volume
docker volume inspect [name] - inspect a volume
```

## Compose

```bash
docker-compose --version - show docker compose version
docker-compose up - build, recreate, start, and attach containers for a service
docker-compose down - stop and remove containers, networks, images and volumes
docker-compose ps - list containers
docker-compose build - build or rebuild services
docker-compose pull - pull service images
docker-compose start - start services
docker-compose stop - stop services
docker-compose restart - restart services
docker-compose logs - view output from containers
```

## Cleaning Up

```bash
docker system prune - remove unused data
docker container prune - remove all stopped containers
docker image prune - remove unused images
docker volume prune - remove all unused volumes
docker network prune - remove all unused networks
```

## Dockerfile Directives

```bash
FROM [image] - base image
COPY [src] [dest] - copy files/directories to container
ADD [src] [dest] - copy files/directories with URL support
RUN [command] - run a command in the container
CMD [command] - set default command to run when container starts
ENTRYPOINT [command] - set the command to run as an entrypoint
EXPOSE [port] - expose a port
ENV [key]=[value] - set environment variable
WORKDIR [dir] - set the working directory
USER [user] - set the user to run the container as
VOLUME [path] - create a mount point with a volume
```



