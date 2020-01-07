# Exercise 1.14

The associated Dockerfile is in this directory.

After building the image with tag `rails` we can start a new container.

    $ docker run -d -p 3000:3000 rails

After this, the webpage in localhost:3000 opens the rails application which counts the presses of the button
in the main page.