#+BEGIN_HTML


** install Docker 

| Install docker on Ubuntu    | =apt-get install docker.io=                                             |
| [Install docker on rehel]]    | [https://docs.docker.com/engine/install/rhel/][Link: How To Install and Use Docker on rehel ]]   |
| Install docker in Debian 10 | [[https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-10][Link: How To Install and Use Docker on Debian 10]]                        |



Container run
Container is runtime environments for an image. When we do docker pull <image>, the container is not started nor created yet.

We most commonly used command is the docker run <image> command. It downloads the image if it's not already in our local machine and starts the container once the image is ready.

docker create: creates a writable container layer over the specified image and prepares it for running the specified command. The container ID is then printed to STDOUT. This is similar to docker run -d except the container is never started. We can then use the docker start <container_id> command to start the container at any point.
$ docker create -t -i fedora bash
...
dff32a272ad4c94cd51419ee4f53c371e3c3a8cfb448a469634d4420e139d118

$ docker start -a -i dff32a272ad4c
[root@dff32a272ad4 /]# 
i: interactive, keep STDIN open even if not attached
t: Allocate a pseudo-TTY
a: Attach container's STDOUT and STDERR and forward all signals to the process.

docker rename allows the container to be renamed.
$ docker rename my_container my_new_container

docker run creates and starts a container in one operation.
$ docker run -it ubuntu-ssh-k /bin/bash

docker rm deletes a container.
$ docker rm myfedora

docker update updates a container's resource limits. Example : updating multiple resource configurations for multiple containers:
$ docker update --cpu-shares 512 -m 300M dff32a272ad4 happy_kare
dff32a272ad4
happy_kare


Container info
docker ps shows running containers.
$ docker ps 
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
e2481c1bad5d        ubuntu-ssh-k:latest   "/bin/bash"         10 hours ago        Up 10 hours                             hopeful_carson 

docker logs gets logs from container. (We can use a custom log driver, but logs is only available for json-file and journald in 1.10)
$ docker logs 839f66a78983

docker inspect looks at all the info on a container (including IP address).
To get an IP address of a running container:
$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' $(docker ps -q)
172.17.0.5

docker events gets events from container.
docker port shows public facing port of container.
docker top shows running processes in container.
docker stats shows containers' resource usage statistics.
docker diff shows changed files in the container's FS.