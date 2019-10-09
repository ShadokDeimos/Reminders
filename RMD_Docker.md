
## INSTALL Docker (Debian)

$ apt-get update

$ apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common

$ curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

	/!\ V�rifier que l'install est faite

$ apt-key fingerprint 0EBFCD88

	Ceci doit s'afficher
>>>
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22

$ add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

## INSTALL DOCKER CE

$ apt-get update

$ apt-get install docker-ce docker-ce-cli containerd.io

$ docker run hello-world

_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

## INSTALLER DOCKER-COMPOSE

$ sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose && sudo chmod +x /usr/bin/docker-compose

_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

## DOCKER COMMANDS

$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
  => main options :
    -d -> detached mode => container run in background
    --name
    -p

    Lance l'instance souhaité


$ docker ps                 List the running containers
$ docker ps -as             List the containers
            -a -> all
            -s -> size

$ docker start -i <ContainerName>
      => Allow to restart a previously stopped container => use for dev and debugging
              -i -> keep STDIN open
              -t -> allocate a tty
              -a=[] -> STDIN, STDOUT, STDERR

    --expose <port>
      => container will be accessible on the specified port by other containers

    --publish
    -p [<IPHost>:]<portHost>:<portContainer>[/<protocol>]
      => container will be available outside the host on the specified port


    --restart=<policy>
        -> no     => Do not automaticcaly restart. Default.
        -> on-failure[:maxretry]      => Restart only if the container exit with a non-zero exit status
        -> always         => Always restart, indefinitely
        -> unless-stopped         => Always restart except if the container was put into a stopped state

$ docker images                 Lists images on the host
                --all, -a       Show all images
                --filter, -f    Filter
                --format        Show a Go template

$ docker image
                build           Build an image from a file
                inspect         Display detailed information
                ls              List images
                pull            Pull an image from a registry
                push            Push an image in a registry
                rm              Remove image

$ docker push           # Need to complete

$ docker volume
                create
                       --driver             Specify volume driver name
                       --label              Set metadata for a volume
                       --name               Specify volume name
                       --opt                Set driver specific options

                inspect           Display detailed information on one or more volumes
                ls                List volumes
                prune             Remove all unused local volumes
                rm                Remove one or more volumes

$ docker build <option> <dir>            Once your Dockerfile is ready
               -f   path and name to Dockerfile (not need if named "Dockerfile")
               -t   tag (name) your image
							 --tag=pouet			name your image
               -m   set memory limit
               -rm  remove intermediate containers after a build

$ docker login
		=> enter login and pass to docker account

$ docker tag image username/repository:tag

	/!\ ON MASTER /!\
$ docker swarm init
$ docker swarm leave --force

	/!\ ON NODE /!\
$ docker join blablabla token etc...

$ docker stack deploy -c docker-compose.yml <servicename>
$ docker stack rm <servicename>
$ docker stack ps <servicename>

$ docker service ls

_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

## Dockerfile

- To create a dockerfile create a "Dockerfile" without extension
.dockerignore   allow to specify wich folders/files will not be taking by Dockerfile instructions
Dockerfile instructions

#             comments
FROM          used to specify the base image
RUN           execute a command in a new layer on top of the image
CMD           command that is executed by default when a container is ran
EXPOSE        informs Docker the port listened by the container (not publish!)
ENV           define enviroment variables
COPY          copy files and folder in the image
ADD           add files and folder in the image
ENTRYPOINT    allow to have arguments at run
WORKDIR				set the working directory

VOLUME        allow to specify the usage of a volume for containers
USER          allow to specify wich user or group will execute RUN, CMD or ENTRYPOINT
HEALTHCHECK   internal check to know if the container works correctly

_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

version: "3"
services:
  web:
    # replace username/repo:tag with your name and image details
    image: username/repo:tag
    deploy:
      replicas: 5
      restart_policy:
        condition: on-failure
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
    ports:
      - "80:80"
    networks:
      - webnet
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]
    networks:
      - webnet
  redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - "/home/docker/data:/data"
    deploy:
      placement:
        constraints: [node.role == manager]
    command: redis-server --appendonly yes
    networks:
      - webnet
networks:
  webnet:
