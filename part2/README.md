# Exercises for part 2

There are separate folders for all the exercises that requires a separate files. Those folders contains the required docker-compose.yml files and associated informations.

## Exercise 2.4

To scale the compute containers up we can use the --scale option

    $ docker-compose up --scale compute=10 -d

Running this command against the docker-compose.yml of this exercise works. The amount of compute
containers was chosen arbitrarily. May be less nodes might suffice.