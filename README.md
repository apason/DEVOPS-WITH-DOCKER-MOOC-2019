# DEVOPS-WITH-DOCKER-MOOC-2019

docker run <image>        :: runs the image with default options
       	   	   -d     :: runs in detached mode
		   --name :: gives a name to container
		   -v     :: localDir:containerDir bind mounts the directory to container
		   	     can also be a single file
		   -p	  :: <hostport>:<containerPort> publishes a port
	 	   -
       e.g. docker run hello-world

docker images | docker image ls :: shows all locally available images

docker rmi <image> :: removes the unused (no containers with reference to it) image
       	   	   - can be forced, but usually bad idea
       e.g. docker rmi hello-world

docker container ls :: lists all active (running) containers
       		    -a :: list all (not necessarily running) containers

docker container prune :: deletes all containers

docker pull <image> :: pulls the image (from dockerHub) withou running
docker pull <path>  :: pulls the image from path without running

docker rm <container>            :: removes the container
       	  	      --force -f :: force remove (e.g. running container)

docker stop <container>   :: stops the running container

docker exec <command>     :: executes a command inside a container



EXERCISE 1:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES
5e1793208d7a        nginx               "nginx -g 'daemon of…"   38 seconds ago       Up 37 seconds               80/tcp              hardcore_curie
ac8b8e5b8ad6        nginx               "nginx -g 'daemon of…"   41 seconds ago       Exited (0) 6 seconds ago                        compassionate_morse
4ac20608a088        nginx               "nginx -g 'daemon of…"   About a minute ago   Exited (0) 17 seconds ago                       heuristic_galileo

EXERCISE 2:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker ps -a ; docker images
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

docker search <name> :: searches image named name from docker hub


EXERCISE 3:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -it devopsdockeruh/pull_exercise                                                                                                         125 ↵
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete 
5e2195587d10: Pull complete 
6f595b2fc66d: Pull complete 
165f32bf4e94: Pull complete 
67c4f504c224: Pull complete 
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"


docker tag <img1:tag1> <img2:tag2> tags(renames) img2:tag2 to img1:tag1

docker logs <container>     :: fetches the logs of container
       	    		 -f :: follow the log output (like tail -f)

docker pause <container>    :: pauses the execution of the container

docker unpause <container>  :: continues the execution of paused container

docker attach <container>   :: attaches the container to given terminal
       	      		  --sig-proxy=false :: disables signal proxying (e.g. C-c) to container

docker exec <container> <command> :: starts a new process in container

EXERCISE 4:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -dit devopsdockeruh/exec_bash_exercise
c2ff8c3ec29bc2eb41a2aa0e64a8f4041145737432ad14d1717e22fa852ffde6

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker exec -it c2f /bin/bash
root@c2ff8c3ec29b:/usr/app# tail -f logs.txt 
Secret message is:
"Docker is easy"


EXERCISE 5:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -it ubuntu sh -c 'apt-get update && apt-get install -y curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'

... ( output of apt-get update and apt-get install omitted) ...

Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>


WORKDIR <full_path>  :: sets the current working directory
RUN <command>        :: runs the command with /bin/sh -c
COPY <file1> <file2> :: copies the local file file1 to the image to file2
CMD  	     	     :: command to run when the container starts
ENTRYPOINT <entrypoint> :: sets the entrypoint for CMD
ENV <variable>=<value>  :: sets the value to the environment variable variable
    			   Takses effect in build process and runtime
EXPOSE <port>		:: exposes a port port to containers from this image

docker build <dir>         :: builds the image from docker file in dir
       	     	  -t <tag> :: Tags a name to the image

docker diff <containerId>  :: displays the difference between container and its source image

docker commit <containerId> <newImageName> :: creates a new image from container

EXERCISE 6:

## start of Dockerfile
FROM devopsdockeruh/overwrite_cmd_exercise

CMD ["-c", "0"]

## end of dockerfile


EXERCISE 7:

## start of Dockerfile
FROM ubuntu
COPY script1.7.sh .
RUN chmod +x script1.7.sh
RUN apt-get update && apt-get install -y curl
CMD ["./script1.7.sh"]

## end of Dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -i curler                                                                                                                                  3 ↵
Input website:
helsinki.fi
Searching..
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   231  100   231    0     0  12157      0 --:--:-- --:--:-- --:--:-- 12833
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>


docker cp <container:fullpath> <localpath> :: copies a file from container to local fs



EXERCISE 8:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤ docker run -v $(pwd)/container.logs:/usr/app/logs.txt devopsdockeruh/first_volume_exercise


EXERCISE 9:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -d -p 1234:80 devopsdockeruh/ports_exercise
Unable to find image 'devopsdockeruh/ports_exercise:latest' locally
latest: Pulling from devopsdockeruh/ports_exercise
cd784148e348: Pull complete 
9abca35fefbf: Pull complete 
7fc670963d22: Pull complete 
893040f9bc16: Pull complete 
b0ae6401e570: Pull complete 
Digest: sha256:2ff93dd0c744aee7a8f00bc9558d09fd6279493da0d01769fe600f78fb4593f2
Status: Downloaded newer image for devopsdockeruh/ports_exercise:latest
cd46a23db6eaedb17933c11d75a7d28aae68c00b244d424fd8a77b95be2ff6c9

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  curl http://localhost:1234
Ports configured correctly!!%

EXERCISE 10:

## start of Dockerfile
FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/frontend-example-docker
WORKDIR /app/frontend-example-docker

RUN npm install

EXPOSE 5000

CMD ["npm", "start"]

## end of dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -p 5000:5000 -d 37df09a407a8

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  curl http://localhost:5000                                                                                                                           56 ↵
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta content="ie=edge" http-equiv="x-ua-compatible">
    <title>Webpack App</title>
    <link href="vendors~main-1.css" rel="stylesheet" />
    <link href="main.css" rel="stylesheet" />
  </head>
  <body>
    <div id="root">
    </div>
    <script src="vendors~main.js" type="text/javascript"></script>
    <script src="main.js" type="text/javascript"></script>
  </body>
</html>

EXERCISE 11:

## start of Dockerfile
FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/backend-example-docker
WORKDIR /app/backend-example-docker

RUN npm install

EXPOSE 8000

CMD ["npm", "start"]
## end of Dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -p 8000:8000 -v $(pwd)/logs.txt:/app/backend-example-docker/logs.txt -d backend

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  curl localhost:8000
Port configured correctly, generated message in logs.txt%

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  cat logs.txt 
1/4/2020, 9:34:11 PM: Connection received in root

EXERCISE 12:

## start of backend Dockerfile
FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/backend-example-docker
WORKDIR /app/backend-example-docker

RUN npm install

EXPOSE 8000

ENV FRONT_URL=http://192.168.1.219:5000

CMD ["npm", "start"]
## end of backend Dockerfile

## start of frontend Dockerfile
FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/frontend-example-docker
WORKDIR /app/frontend-example-docker

RUN npm install

EXPOSE 5000

ENV API_URL=http://192.168.1.219:8000

CMD ["npm", "start"]
## end of frontend Dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -p 8000:8000 -v $(pwd)/logs.txt:/app/backend-example-docker/logs.txt -d backend

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -p 5000:5000 -d frontend

EXERCISE 13:

## start of Dockerfile
FROM openjdk:8

WORKDIR /app

RUN apt-get update && apt-get install -y curl git

RUN git clone https://github.com/docker-hy/spring-example-project

WORKDIR /app/spring-example-project

RUN ./mvnw package

EXPOSE 8080

CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]
## end of Dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -p 8080:8080 ex13

Exercise 14:

## start of Dockerfile
FROM ruby:2.6.0

WORKDIR /app

RUN apt-get update && apt-get install -y git nodejs

RUN gem install bundler

RUN git clone https://github.com/docker-hy/rails-example-project

WORKDIR /app/rails-example-project

RUN bundle install

RUN rails db:migrate

EXPOSE 3000

CMD ["rails", "s"]
## end of Dockerfile

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019  ‹master*› 
╰─➤  docker run -d -p 3000:3000 rails

EXERCISE 15:

See https://hub.docker.com/repository/docker/apason/simplex

Exercise 16:

https://heroku-example-mooc.herokuapp.com


Problems and solutions for docker-compose:

volumes: When you use a named volume, like "data:/cjworkbench:rw" you must declare it at the docker-compose file
 However using just path can be done giving relative or full path.

EXERCISE 2.1

version: "3.7"
services:
  logger:
    image: devopsdockeruh/first_volume_exercise
    volumes:
      - ./:/usr/app/helper
    command: bash -c "touch helper/logs.txt && rm logs.txt && ln -s helper/logs.txt logs.txt && node index.js"

EXERCISE 2.2:

version: '3.5'  

services: 
    ports_exercise: 
      image: devopsdockeruh/ports_exercise
      ports: 
        - 80:80


EXERCISE 2.3:

assuming the dockerfiles are in the same folder named backend.Dockerfile and frontend.Dockerfile

version: '3.5'  

services:

    backend:
      build:
        context: .
        dockerfile: backend.Dockerfile
      image: backend
      ports:
       - 8000:8000
      volumes:
       - ./logs.txt:/app/backend-example-docker/logs.txt

    frontend:
      build:
        context: .
        dockerfile: frontend.Dockerfile
      image: frontend
      ports:
       - 5000:5000


EXERCISE 2.4:

╭─apa@turbopenis ~/DEVOPS-WITH-DOCKER-MOOC-2019/scaling-exercise  ‹master› 
╰─➤  docker-compose up --scale compute=10 -d


EXERCISE 2.5:

version: '3.5'  

services:

    backend:
      build:
        context: .
        dockerfile: backend.Dockerfile
      image: backend
      ports:
       - 8000:8000
      volumes:
       - ./logs.txt:/app/backend-example-docker/logs.txt
      environment:
       - REDIS=redis

    frontend:
      build:
        context: .
        dockerfile: frontend.Dockerfile
      image: frontend
      ports:
       - 5000:5000


    redis:
      image: redis


EXERCISE 2.6:


version: '3.5'  

services:

    backend:
      build:
        context: .
        dockerfile: backend.Dockerfile
      image: backend
      ports:
       - 8000:8000
      volumes:
       - ./logs.txt:/app/backend-example-docker/logs.txt
      environment:
       - REDIS=redis
       - DB_USERNAME=postgres
       - DB_PASSWORD=example
       - DB_HOST=db
      depends_on:
       - redis
       - db
      restart: unless-stopped

    frontend:
      build:
        context: .
        dockerfile: frontend.Dockerfile
      image: frontend
      ports:
       - 5000:5000

    redis:
      image: redis

    db:
      image: postgres
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: example
      container_name: db_backend
      volumes:
       - database_backend:/var/lib/postgresql/data



volumes:
  database_backend:



EXERCISE 2.7:



EXERCISE 2.8:

version: '3.5'  

services:

    backend:
      build:
        context: .
        dockerfile: backend.Dockerfile
      image: backend
      ports:
       - 8000:8000
      volumes:
       - ./logs.txt:/app/backend-example-docker/logs.txt
      environment:
       - REDIS=redis
       - DB_USERNAME=postgres
       - DB_PASSWORD=example
       - DB_HOST=db
      depends_on:
       - redis
       - db
      restart: unless-stopped

    frontend:
      build:
        context: .
        dockerfile: frontend.Dockerfile
      image: frontend
      ports:
       - 5000:5000

    redis:
      image: redis

    db:
      image: postgres
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: example
      container_name: db_backend
      volumes:
       - database_backend:/var/lib/postgresql/data

    proxy:
      image: nginx
      volumes:
       - ./nginx.conf:/etc/nginx/nginx.conf
      ports:
       - 80:80
      restart: unless-stopped
      depends_on:
       - backend
       - frontend

volumes:
  database_backend:


EXERCISE 9:

already done in previous

EXERCISE 10:

## start of frontend Dockerfile

FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/frontend-example-docker
WORKDIR /app/frontend-example-docker

RUN npm install

EXPOSE 5000

ENV API_URL=http://localhost/api/

CMD ["npm", "start"]

## end of frontend Dockerfile

## start of backend Dockerfile

FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/backend-example-docker
WORKDIR /app/backend-example-docker

RUN npm install

EXPOSE 8000

ENV FRONT_URL=http://localhost

CMD ["npm", "start"]

## end of backend Dockerfile

## start of docker-compose.yml

version: '3.5'  

services:

    backend:
      build:
        context: .
        dockerfile: backend.Dockerfile
      image: backend
      ports:
       - 8000:8000
      volumes:
       - ./logs.txt:/app/backend-example-docker/logs.txt
      environment:
       - REDIS=redis
       - DB_USERNAME=postgres
       - DB_PASSWORD=example
       - DB_HOST=db
      depends_on:
       - redis
       - db
      restart: unless-stopped

    frontend:
      build:
        context: .
        dockerfile: frontend.Dockerfile
      image: frontend
      ports:
       - 5000:5000

    redis:
      image: redis

    db:
      image: postgres
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: example
      container_name: db_backend
      volumes:
       - database_backend:/var/lib/postgresql/data

    proxy:
      image: nginx
      volumes:
       - ./nginx.conf:/etc/nginx/nginx.conf
      ports:
       - 80:80
      restart: unless-stopped
      depends_on:
       - backend
       - frontend

volumes:
  database_backend:

## end of docker-compose.yml
