# Exercise 2.9

This exercise is otherwise same as the last one but there is database volume defined.
All needed files are located in this directory. I could not find how to define the path
to the database using the relative path `./database`. For this reason the directory
is defined using absolute path.

After creating the ./database folder and starting with docker-compose up the frontend
allows to save strings into the database. After restarting the data is still available.

After removing and recreating the database folder, the data is also gone.