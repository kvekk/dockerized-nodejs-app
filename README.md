# Dockerizing a Node.js web app
This application was based on [Node.js documentation guide](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/) on dockerizing a Node.js web app.
## Building a Docker image
1. Get the source: _git clone https://github.com/kvekk/dockerized-nodejs-app.git_
2. Move into downloaded repo: _cd dockerized-nodejs-app/_

3. Finally,  run the following command to build the Docker image. The _-t_ flag lets you tag your image so it's easier to find later using the _docker images_ command:
```sh
docker build . -t <your username>/node-web-app
```
Here is the way I did it:
```sh
docker build . -t kvekk/nodejs-app
```
## Running the image
```sh
docker run -d -p 80:80 -m 256m --cpus="1" --name nodejs-app --rm kvekk/nodejs-app
```
- _-d_ : runs the container in detached mode, leaving the container running in the background
- _-p_ : redirects a public port to a private port inside the container
- _-m_ : limits memory. In the example above it limits it to 256 megabytes.
- _--cpus_ : specifies how much of the available CPU resources a container can use. For instance, if the host machine has two CPUs and you set _--cpus="1.5"_, the container is guaranteed at most one and a half of the CPUs.
- _--name_ : sets a custom name for the container.
- _--rm_ : automatically removes the container when it exits.

After running the image, you can go to http://localhost:80/ and see the result.
To attempt to gracefully shutdown your container, run:
```sh
docker stop nodejs-app
```
To immediately stop/terminate it, run:
```sh
docker kill nodejs-app
```
## Pushing your image to Docker Hub
1. docker login
2. docker push <image_name>:latest
## Pulling images from Docker Hub
To pull [my prebuild image](https://hub.docker.com/r/kvekk/nodejs-app) of this sample application:
```sh
docker pull kvekk/nodejs-app:latest
```