# Exercise 1.12

The Dockerfiles for frontend and backend are in this directory.

The image `backend` is built from the file backend.Dockerfile and the image `frontend` is build from the file
frontend.Dockerfile. After the build we run the images with ports correct ports. In addition the backend has a logs.txt
file bind mounted to the container.


    $ touch logs.txt && docker run -p 8000:8000 -v $(pwd)/logs.txt:/app/backend-example-docker/logs.txt -d backend
    $ docker run -p 5000:5000 -d frontend

After this the the button for 1.12 turns green in localhost:5000