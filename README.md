# docker-note


=== images ===
# login to docker hub
	> docker login

# search images from registries
	> docker search image-name

# pull image
	> docker pull image-name

# show downloaded images
	> docker images

# create image from container
	> docker commit container-name image-name:tag-name

# push images to personal registries
	> docker tag my-ubuntu user-id/image-name
	> docker push user-id/image-name

# remove image
	> docker rmi image-name:tag-name


=== containers ===
# show running containers
	> docker ps

# show all containers, including running and stopped containers
	> docker ps -a

# show logs from container
	> docker logs container-name

# put running container into stopped state
	> docker kill container-name

# restart stopped container
	> docker start container-id
	
# attach container
	> docker attach container-id

# remove stopped container
	> docker rm container-id


=== networks ===
# show networks
	> docker network ls

# create new network
	> docker network create network-name

# show exposing ports of the container
	> docker port container-name
	

=== run ===
# start a running container from image
# --rm: remove container after exit
# -ti: terminal interactive mode
# --name: give this container a name for future reference
> docker run --rm -ti --name testA my-ubuntu bash

# runs a new command in a running container
> docker exec -ti testA bash

# -d: detached mode
> docker run -d --name testA my-ubuntu bash -c "sleep 5; echo hahaha"

# -e: set environment variables for container
> docker run --rm -ti -e ENV=DEV --name testA my-ubuntu bash

# -p: expose port, 4321/tcp -> 0.0.0.0:1234
> docker run --rm -ti -p 1234:4321 --name testA my-ubuntu bash

# --net: put container into certain network
> docker run --rm -ti --net network-name --name testA my-ubuntu bash

# -v: volumes, share data between host and container
> docker run --rm -ti -v D:/docker-data:/shared-folder --name testA my-ubuntu bash

# --volumes-from: share data between containers
> docker run --rm -ti -v /shared-folder --name testA my-ubuntu bash
> docker run --rm -ti --volumes-from testA --name testB my-ubuntu bash


=== Dockerfile ===
# building images with code
> docker build -t image-name

ex:
	FROM ubuntu
	RUN apt -y update
	RUN apt -y install vim fish
	ADD banner.txt /banner.txt
	CMD cat /banner.txt && fish

