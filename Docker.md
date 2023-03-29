

## Build image and run container

```sh 
$ docker build -t dashboard-back .

$ docker images
REPOSITORY                             TAG                  IMAGE ID       CREATED          SIZE
dashboard-back                         latest               c6abc98489ac   10 seconds ago   503MB

$ docker run -p 8080:8080 dashboard-back
 ``` 
  
## Restart container

```sh 
$ docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED        STATUS          PORTS                                       NAMES
a8d88c7291f0   postgres   "docker-entrypoint.s…"   2 months ago   Up 52 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   venus

$ docker stop  a8d88c7291f0
a8d88c7291f0

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker restart venus
venus

$ docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED        STATUS         PORTS                                       NAMES
a8d88c7291f0   postgres   "docker-entrypoint.s…"   2 months ago   Up 3 seconds   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   venus
```


## Remove container

```sh 
$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED          STATUS                      PORTS                                    NAMES
31592bd9c6d9   d893473a6510   "/bin/sh -c '\n# bloc…"   13 minutes ago   Exited (1) 12 minutes ago                                            appolo_11
7fd4c88d6a4d   d893473a6510   "/etc/confluent/dock…"    13 minutes ago   Exited (1) 13 minutes ago                                            mars_2023
a8d88c7291f0   venus       "docker-entrypoint.s…"    5 weeks ago      Up 5 hours                  0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   venus

$ docker rm -f 31592bd9c6d9  7fd4c88d6a4d
31592bd9c6d9
7fd4c88d6a4d

$ docker ps -a
CONTAINER ID   IMAGE      COMMAND                  CREATED       STATUS       PORTS                                    NAMES
a8d88c7291f0   venus   "docker-entrypoint.s…"   5 weeks ago   Up 5 hours   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   venus
```

## Remove all stopped containers 
```sh 
$ docker rm $(docker ps --filter status=exited -q)
 ```
 
 
## Remove all containers and images

to remove all the Docker containers running on machine:
```sh 
$ docker rm -f $(docker ps -qa)
``` 
and then remove the Docker images:
```sh 
$ docker rmi -f $(docker images -aq)
```



## How to delete all docker containers except one:
Solution 1:

The alternative solution bases on cut that cuts the first column from ps -> grep result.

```sh 
$ docker container ls | grep -v "docker_container_ID_here" | cut -f 1 -d ' '
$ docker container rm $(docker container ls | grep -v "docker_container_ID_here" | cut -f 1 -d ' ')
```
How it works:
- docker container ls prints all containers,
- grep -v "docker_container_ID_here" prints the lines that don't, match docker_container_ID_here,
- cut -f 1 -d ' ' prints only first column,
- docker rm $(...) removes all containers.
source: https://dirask.com/posts/Docker-remove-all-containers-except-one-1RPyMp

Solution 2:
```sh 
$ docker ps -aq | grep -v <container_id_or_name> | xargs docker rm -f
 ```
 
The command is a shell command that can be used to delete all Docker containers except the one specified by its ID or name.

Here is what each part of the command does:
- docker ps -aq: Lists all running and stopped containers in a quiet mode, which only displays the container IDs.
- grep -v <container_id_or_name>: Filters out the container specified by its ID or name using the -v option, which tells grep to exclude the matching lines.
- xargs docker rm -f: Takes the container IDs passed from the previous command and runs the docker rm -f command on each of them, which forcibly removes the containers.

Replace <container_id_or_name> with the actual ID or name of the container you want to keep.












## Access a shell inside a running Docker container
By running the command 
```sh 
$ docker container exec -it <container_name/id> bash
```
you can access a Bash shell within a running Docker container.
This allows you to execute commands within the container's environment. 

