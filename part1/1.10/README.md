# Exercise 1.10

The associated Dockerfile is in this directory.

After building the container with tag `frontend`

    $ docker run -p 5000:5000 -d frontend

    $ curl http://localhost:5000
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

We can see that the website is up and running.