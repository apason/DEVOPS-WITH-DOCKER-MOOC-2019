# Exercise 2.1

This exercise has the definition "make sure that it works simply by running `docker-compose up` so we can not
first create the logs.txt file and bind mount it as a file like in the exercises in part 1. (non-existing
host paths for bind mounts are always created as a *directory*, not as a *file*. 

Because the trivial approach (create the logfile file before starting the container) is out of the question (the
file cannot be created from the docker-compose.yml), we need
something else. This could be done using a volume but in my opinion it is not a good solution because the location
of the volume may depend on the operating systems and the docker versions. Technically however, the log file is in
the container which is in "my filesystem" so technically it suffices to just run the image 
devopsdockeruh/first_volume_exercise via the docker-compose.yml file.

In my solution the starting command of the image is overwritten by docker-compose. The default run command 
`node index` (inspected from a container) is replaced with 

    bash -c "touch helper/logs.txt && rm logs.txt && ln -s helper/logs.txt logs.txt && node index"

Now when the container is started with current working directory bind mounted to /usr/app/helper we can create
the problematic log file to the local filesystem. When we make a symlink to the original logs.txt in the container
and then start the original starting command `node index` the logs are actually written to the new local file $PWD/logs.txt