README
======
This is an example of a Docker container running a minimal Rails App. 
The example app consists of an empty welcome controller only and is
is using SQLite. It is served by Ningx and Unicorn. 

The Rails app is called SimpleApp, the repository `simple-app`, and the
description below calls the Docker image `example:simple_app`. Obviously,
the use of hyphens vs underscores is somewhat inconsistent.

Files
-----
The relevant files for this Docker example are

1. Dockerfile,
2. config/unicorn.rb (sets up stuff),
3. config/simple-app.conf (template for nginx config file),
4. config/start_file.sh (a template for starting unicorn and nginx).

Getting to a running Docker container
-------------------------------------
Getting the example Rails app took the following steps.

(1) Write docker file to include all depencies (Dockerfile).

(2) Write start-up script for unicorn and nginx (cf. config/start_file.sh).

(3) Write a unicorn config file for rails app (cf. config/simple-app.conf)

(4) Build docker image.

```
docker build -t examples:simple_app .
```

Note: I had to set the environment variable for `config/secrets.yml`. 

(5) Run the image binding the hosts port 80 to the client's.

```
docker run -p 80:80 -t examples:simple_app
```

Some useful Docker commands
---------------------------
When debuging I found it useful to log into the Docker container using

```
docker exec -it <container id> bash
```

Get running current containers' ids with `docker ps` and use that id to `docker kill` them.

Remove all images with `docker rmi $(docker images -q)`.

Running on OS X I got the ip of the boot2docker VM by `boot2docker ip`.
