# Exercises for part 1

There are separate folders for those exercises where dockerfiles were required. The answers for first
exercises (no Separate dockerfiles) is written in this file.

## Exercise 1.1

After starting three nginx container and shutting two of them down, the output is

    $ docker ps -a
    CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES
    5e1793208d7a        nginx               "nginx -g 'daemon of..."   38 seconds ago       Up 37 seconds               80/tcp              hardcore_curie
    ac8b8e5b8ad6        nginx               "nginx -g 'daemon of..."   41 seconds ago       Exited (0) 6 seconds ago                        compassionate_morse
    4ac20608a088        nginx               "nginx -g 'daemon of..."   About a minute ago   Exited (0) 17 seconds ago                       heuristic_galileo
    
## Exercise 1.2

After cleaning all docker containers and images

    $ docker ps -a ; docker images
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  
## Exercise 1.3

The password defined in the documentation of devopsdockeruh/pull_exercise repository is "_basics_".
Entering it to the started container yelds the secret message "_This is the secret message_".

    $ docker run -it devopsdockeruh/pull_exercise
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

## Exercise 1.4

The secret message of this exercise is "_Docker is easy_"

    $ docker run -dit devopsdockeruh/exec_bash_exercise
    c2ff8c3ec29bc2eb41a2aa0e64a8f4041145737432ad14d1717e22fa852ffde6
  
    $ docker exec -it c2f /bin/bash
    root@c2ff8c3ec29b:/usr/app# tail -f logs.txt 
    Secret message is:
    "Docker is easy"

## Exercise 1.5

The container needs curl so the installation can be run before the actual curl request.

    $ docker run -it ubuntu sh -c 'apt-get update && apt-get install -y curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
    
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

