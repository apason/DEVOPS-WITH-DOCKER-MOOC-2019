# Exercise 1.7

The related Dockerfile and the associated script file are in this directory.

Running the container yelds the same result with the exercise 1.5

    $ docker run -i curler
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

