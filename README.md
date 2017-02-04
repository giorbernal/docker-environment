

DEVELOPMENT ENVIRONMENT USING DOCKER CONTAINERS
===============================================

This directory contains a development environment configuration with docker. 


Quick start guide for the impatient
-----------------------------------

### Step 1: Install Docker

[Install Docker][Docker-installation]


### Step 2: Install Docker Compose

[Install Docker Compose][Docker-compose-installation]


### Step 3: Create container directories

```sh
$ sudo mkdir -vp /srv/container/{consul,fluentd,rabbitmq,mongo,elasticsearch,redis,cassandra}
```

### Step 4. Start/Stop containers

```sh
$ docker-compose up -d [<service_name>]
$ docker-compose stop [<service_name>]
```

### The following services are available

* [Consul](https://www.consul.io/intro/index.html)
* [Fluentd](http://www.fluentd.org/architecture)
* [RabbitMq](http://www.rabbitmq.com/getstarted.html)
* [Mongo](https://docs.mongodb.com/manual/introduction/)
* [Elasticsearch](https://www.elastic.co/)
* [Cassandra](http://cassandra.apache.org/)
* [Redis](http://try.redis.io/)

[Docker-installation]: https://docs.docker.com/engine/installation/
[Docker-compose-installation]: https://docs.docker.com/compose/install/

### Avoid sudo usage

#### 1. Add the docker group

```sh
$ sudo groupadd docker
```

#### 2. Add self user to the docker group

```sh
$ sudo usermod -a -G docker <username>
```

#### 3. Restart docker daemon

```sh
$ sudo service docker restart
```

#### 4. Logout and login again

```sh
$ exit
```


Getting started with docker
---------------------------

Docker provides a containerization platform that allows developers to build and ship lightweight, portable containers
that can be run anywhere and anytime in an easily way.


### Containers

Containers are to Virtual Machines as threads are to processes. They contain the application and all of its dependencies.
Docker containers are not tied to any specific infrastructure, they run on any computer.

#### Lifecycle

* [`docker create`](https://docs.docker.com/engine/reference/commandline/create) creates a container but does not start it.
* [`docker rename`](https://docs.docker.com/engine/reference/commandline/rename/) allows the container to be renamed.
* [`docker run`](https://docs.docker.com/engine/reference/commandline/run) creates and starts a container in one operation.
* [`docker rm`](https://docs.docker.com/engine/reference/commandline/rm) deletes a container.
* [`docker update`](https://docs.docker.com/engine/reference/commandline/update/) updates a container's resource limits.

If you want a transient container, `docker run --rm` will remove the container after it stops.

If you want to map a directory on the host to a docker container, `docker run -v $HOSTDIR:$DOCKERDIR`.

If you want to remove also the volumes associated with the container, the deletion of the container must include the `-v` 
switch like in `docker rm -v`.

#### Starting and Stopping

* [`docker start`](https://docs.docker.com/engine/reference/commandline/start) starts a container.
* [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) stops a running container.
* [`docker restart`](https://docs.docker.com/engine/reference/commandline/restart) stops and starts a container.
* [`docker pause`](https://docs.docker.com/engine/reference/commandline/pause/) pauses a running container, "freezing" 
it in place.
* [`docker unpause`](https://docs.docker.com/engine/reference/commandline/unpause/) will unpause a running container.
* [`docker wait`](https://docs.docker.com/engine/reference/commandline/wait) blocks until running container stops.
* [`docker kill`](https://docs.docker.com/engine/reference/commandline/kill) sends a SIGKILL to a running container.

#### Info

* [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps) shows running containers.
* [`docker logs`](https://docs.docker.com/engine/reference/commandline/logs) gets logs from container. 
* [`docker inspect`](https://docs.docker.com/engine/reference/commandline/inspect) looks at all the info on a container 
(including IP address).
* [`docker events`](https://docs.docker.com/engine/reference/commandline/events) gets events from container.
* [`docker port`](https://docs.docker.com/engine/reference/commandline/port) shows public facing port of container.
* [`docker top`](https://docs.docker.com/engine/reference/commandline/top) shows running processes in container.
* [`docker stats`](https://docs.docker.com/engine/reference/commandline/stats) shows containers' resource usage statistics.
* [`docker diff`](https://docs.docker.com/engine/reference/commandline/diff) shows changed files in the container's FS.

`docker ps -a` shows running and stopped containers.

`docker stats --all` shows a running list of containers.

#### Import / Export

* [`docker cp`](https://docs.docker.com/engine/reference/commandline/cp) copies files or folders between a container and 
the local filesystem and vice versa.

#### Executing Commands

* [`docker exec`](https://docs.docker.com/engine/reference/commandline/exec) to execute a command in container.

To enter a running container, attach a new shell process to a running container, e.g.: `docker exec -it foo /bin/bash`.


### Images

Images are just [templates for docker containers](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work).

#### Lifecycle

* [`docker images`](https://docs.docker.com/engine/reference/commandline/images) shows all images.
* [`docker build`](https://docs.docker.com/engine/reference/commandline/build) creates image from Dockerfile.
* [`docker commit`](https://docs.docker.com/engine/reference/commandline/commit) creates image from a container, pausing 
it temporarily if it is running.
* [`docker rmi`](https://docs.docker.com/engine/reference/commandline/rmi) removes an image.

If you want to persist all changes performed into a running container `docker commit` will create a new image based on it.

#### Info

* [`docker history`](https://docs.docker.com/engine/reference/commandline/history) shows history of image.
* [`docker tag`](https://docs.docker.com/engine/reference/commandline/tag) tags an image to a name (local or registry).


### Registry & Repository

A repository is a collection of tagged images that create the file system for a container altogether.

A registry is a server that stores repositories and provides an HTTP API for 
[manage the uploading and downloading of repositories](https://docs.docker.com/engine/tutorials/dockerrepos/).

Docker.com hosts its own [index](https://hub.docker.com/) to a central registry which contains a large number of repositories.  

* [`docker login`](https://docs.docker.com/engine/reference/commandline/login) to login to a registry.
* [`docker logout`](https://docs.docker.com/engine/reference/commandline/logout) to logout from a registry.
* [`docker search`](https://docs.docker.com/engine/reference/commandline/search) searches registry for image.
* [`docker pull`](https://docs.docker.com/engine/reference/commandline/pull) pulls an image from registry to local machine.
* [`docker push`](https://docs.docker.com/engine/reference/commandline/push) pushes an image to the registry from local 
machine.

#### Run local registry

In order to use a local registry check [docker distribution](https://github.com/docker/distribution) project and 
look at the [local deploy](https://github.com/docker/docker.github.io/blob/master/registry/deploying.md) instructions.

### Volumes

[Docker volumes](https://docs.docker.com/engine/tutorials/dockervolumes/) are special directories that provide 
persistent data storage through containers lifecycle. They don't have to be connected to a particular container.  

#### Lifecycle

* [`docker volume create`](https://docs.docker.com/engine/reference/commandline/volume_create/)
* [`docker volume rm`](https://docs.docker.com/engine/reference/commandline/volume_rm/)

### Info

* [`docker volume ls`](https://docs.docker.com/engine/reference/commandline/volume_ls/) lists all volumes docker knows about
* [`docker volume inspect`](https://docs.docker.com/engine/reference/commandline/volume_inspect/)

You can mount them in several docker containers at once, using `docker run --volumes-from`.

Docker-compose reference
------------------------
Docker-compose is a tool that allow us to define and run several docker containers. The configuration is stored in a yaml
file describing all services and applications involved and linked together (if related). When one service is invoked, all 
related services starts in correct order.

### Starting and stopping

* [`docker-compose up`](https://docs.docker.com/compose/reference/up/) builds, creates, starts and attaches to containers 
for a service. It accepts a service name to start. Without service name, docker-compose starts all services defined in file. 
* [`docker-compose stop`](https://docs.docker.com/compose/reference/up/)
* [`docker-compose ps`](https://docs.docker.com/compose/reference/ps/) shows running containers

By default, docker-compose looks for a docker-compose.yml file located in working directory, to specify another filename
and/or path use -f <filename> modifier. E.g. ```docker-compose -f /path/to/my/custom/docker-compose-file.yml up```

-d modifier starts services in detached mode (background)

### Repository

* [`docker-compose pull`](https://docs.docker.com/compose/reference/pull/) pulls service image associated. 

### Cleanup

* [`docker-compose rm`](https://docs.docker.com/compose/reference/rm/) removes stopped service containers. With -vf modifier
also removes anonymous volumes attached to containers.


Useful commands
---------------

### See running container logs until SIGINT

```sh 
$ docker logs -f <container_name>
```

### Delete old containers

```sh
$ docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs docker rm
```

### Kill running containers

```sh
docker ps -q|xargs docker kill
```

### Delete dangling images

```
$ docker images -q -f dangling=true|xargs docker rmi
```

### Delete dangling volumes

```
$ docker volume ls -q -f dangling=true|xargs docker volume rm
```

### To check the CPU, memory, and network I/O usage of a single container

```
$ docker stats <container>
```
