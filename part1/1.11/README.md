# Exercise 1.11

The associated Dockerfile is in this directory.

After building the image with a tag `backend` we need to create the logs.txt in order to mount in as a file.

    $ touch logs.txt && docker run -p 8000:8000 -v $(pwd)/logs.txt:/app/backend-example-docker/logs.txt -d backend

    $ curl localhost:8000
    Port configured correctly, generated message in logs.txt%

    $ cat logs.txt 
    1/4/2020, 9:34:11 PM: Connection received in root

