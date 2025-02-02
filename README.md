# Inception

This project aims to broaden your knowledge of system administration by using Docker. You will virtualize several Docker images, creating them in your new personal virtual machine.
# Docker

Docker is an open source platform that enables developers to build, deploy, run, update and manage containers—standardized, executable components that combine application source code with the operating system (OS) libraries and dependencies required to run that code in any environment

<img width="335" alt="Screen Shot 2023-01-01 at 4 04 12 PM" src="https://user-images.githubusercontent.com/69278312/210175288-4ac2bc2d-ff19-4a8b-aefe-56113eed2969.png">
 
- display information about your Docker environment:

        docker info
- the version of Docker:

        docker --version
- lists the running containers on your system:

        docker ps

# Docker containers

After you run a docker image, it creates a docker container. All the applications and their environment run inside this container. You can use Docker API or CLI to start, stop, delete a docker container.

<img width="445" alt="Screen Shot 2023-01-01 at 4 02 36 PM" src="https://user-images.githubusercontent.com/69278312/210175369-9076eda2-ce97-4cc5-9992-5a26fa194eae.png">

- Below is a sample command to run a ubuntu docker container:
        
        docker run -i -t ubuntu /bin/bash
        
- Showing their container IDs, names, status:
        
        docker container ls
        docker container ls -aq
        docker container ls -a
- stop a running container:
        
        docker container stop id or name 
-  Remove one or more containers:
       
        docker container rm -f id or name
        docker container prune
- Run a command in a running container:
        
        docker exec -it id or name bash
- inspect a Docker container:

        docker container inspect id
- Restart one or more running containers:

        docker container restart id or name
 
- docker container logs:

        docker container logs id or name 
   
 # Volumes
 
The persistent storage location that is independent of a container's lifecycle. Volumes can be used to store data that needs to persist even when the container is stopped or removed.

- Create a volume:

        docker volume create --name my-volume
        docker volume create --name my-volume --driver local

- List volumes:
        
        docker volume ls
        
        
- Display detailed information about a volume:

        docker volume inspect my-volume

- Remove one or more volumes

        docker volume rm -f my-volume another-volume

- Remove all unused volumes:

        docker volume prune

- Attach a volume to a container:

        docker run -d --name my-container -v my-volume:/app/data alpine

- Detach a volume from a container:
        
        docker stop my-container && docker rm my-container
      
  # Networks
   - Bridge: It is the default network driver for a container. You use this network when your application is running on standalone containers, i.e. multiple containers communicating with same docker host.
  
   - Host: This driver removes the network isolation between docker containers and docker host. It is used when you don’t need any network isolation between host and container.
  
   - Overlay: This network enables swarm services to communicate with each other. It is used when the containers are running on different Docker hosts or when swarm services are formed by multiple applications.
  
   - None: This driver disables all the networking.
  
   - macvlan: This driver assigns mac address to containers to make them look like physical devices. The traffic is routed between containers through their mac addresses. This network is used when you want the containers to look like a physical device, for example, while migrating a VM setup.
Docker networking is a passage through which all the isolated container communicate. There are mainly five network drivers in docker:

- Create a new network:

          docker network create my-network
- Inspect a network:

          docker network inspect my-network
- Delete a network:

          docker network rm my-network
- Connect a container to a network:

          docker network connect my-network my-container
- Disconnect a container from a network:
          
          docker network disconnect my-network my-container

# Docker images

A read-only template for creating containers. An image contains the installations of an application instance or an instance group with its software and dependencies, and the process to run when the container is launched. 

- list the images on your system:

            docker image ls
- docker image build -t my-image

            docker image build -t my-image .
- pull an image from a registry:

            docker image pull ubuntu
- push an image to a registry:

            docker image push my-image
- remove an image:

            docker image rm -f my-image
- inspect an image:

            docker image inspect my-image
- docker image inspect my-image

            docker image inspect my-image

# DockerFile

Dockerfile is a text file that contains instructions for building a Docker image. It specifies the base image to use, the packages and dependencies to install, the files and directories to include, and any other configurations needed to create a container image.

simple example:

            FROM ubuntu:20.04

            RUN apt-get update && apt-get install -y nginx

            COPY index.html /var/www/html/

            ENTRYPOINT ["nginx", "-g", "daemon off;"]
 - To build an image from a Dockerfile:
 
            docker image build -t my-image .
list of common instructions that you can use in a Dockerfile:
            
  - 'FROM': Specifies the base image to use for the container.
  - 'RUN': Executes a command and creates a new layer on top of the base image.
  - 'CMD': Specifies the default command to run when the container starts.
  - 'ENTRYPOINT': Specifies the default command to run when the container starts, with arguments passed as parameters.
  - 'ENV': Sets an environment variable in the container.
  - 'EXPOSE': Exposes a port or a range of ports for the container.
  - 'WORKDIR': Sets the working directory for the commands in the container.
  - 'COPY': Copies files or directories from the host to the container.
  - 'ADD': Copies files or directories from the host to the container and can automatically decompress compressed files.
  - 'USER': Sets the default user for the container.
  - 'ARG': Defines a build-time variable for the image.

# Docker client

Primary user interface for the Docker daemon. It accepts commands from the user and communicates with the Docker daemon. The Docker daemon and client can run on the same or separate systems. The Docker client and daemon communicate via sockets or through RESTful APIs.

# Docker daemon

Builds, runs, and manages Docker containers on a host machine.
# Docker registries
Repositories of images for users to upload or download. Registries can be public or private. The public Docker registry is called the Docker Hub.
# Docker Architecture

<img width="616" alt="Screen Shot 2023-01-01 at 3 53 27 PM" src="https://user-images.githubusercontent.com/69278312/210174963-b3d94151-7871-4914-b9cf-15739f8c9ae3.png">

# Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to define the services that make up your application in a single file, and then start and stop the entire application with a single command.

- example :

            version: '3'
            services:
              web:
                build: .
                ports:
                  - "8000:8000"
                depends_on:
                  - db
              db:
                image: postgres
                environment:
                  POSTGRES_USER: user
                  POSTGRES_PASSWORD: password

- start the services

               docker-compose up
- stop the services

                docker-compose down
# Nginx
- What is Nginx 
  
   open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more. It started out as a web server designed for maximum performance and stability. In addition to its HTTP server capabilities, NGINX can also function as a proxy server for email (IMAP, POP3, and SMTP) and a reverse proxy and load balancer for HTTP, TCP, and UDP servers.
  
- Nginx lifecycle

・The master process reads the config and binds the port

・The master process launches the worker processes

・The workers start listening and process requests

・When the config is reloaded, new workers are created and replace the old workers

・The master process is dropped and processing ends.

<img width="752" alt="Screen Shot 2023-01-18 at 3 06 56 PM" src="https://user-images.githubusercontent.com/69278312/213192311-15e6b2b3-c54b-44e0-a4fa-085acf0c1464.png">

- What is PHP FPM
is an alternative PHP FastCGI implementation with some additional features useful for sites of any size, especially busier sites. It allows for handling of PHP processes in an optimized way, improving the performance of PHP applications
・PHP FastCGI Process Manager

- PHP file acquisition flow

<img width="752" alt="Screen Shot 2023-01-18 at 3 10 41 PM" src="https://user-images.githubusercontent.com/69278312/213193128-3b9c23f5-81e7-4533-8812-88ade880ef2f.png">

- Flow of static file acquisition

<img width="752" alt="Screen Shot 2023-01-18 at 3 11 34 PM" src="https://user-images.githubusercontent.com/69278312/213193319-bbf0634c-386a-42a7-b200-f89f8f8d2d6e.png">

