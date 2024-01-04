### Chapter 5 - Graphical Apps

## Introduction

Most of the time containers are used for background services that listen on a port. What if you want to run a GUI (graphical user interface) app? There are a few techniques that can be used to run these apps. One of them involves setting up a remote server using [VNC](https://en.wikipedia.org/wiki/Virtual_Network_Computing) to listen on the container's port. Then, using a VNC client on the host, you can view visually interact with the application.

### Firefox

First, create a directory and add a `Dockerfile`

```bash
mkdir ~/firefox-docker
cd ~/firefox-docker
```

```bash
# Dockerfile
FROM ubuntu:latest
RUN apt update && apt install -y x11vnc xvfb firefox
RUN echo "exec firefox" > ~/.xinitrc && chmod +x ~/.xinitrc
CMD ["/usr/bin/x11vnc", "-create", "-forever"]
```

Now add a `docker-compose.yml` file to the same directory

```yaml
# docker-compose.yml
# usage: docker-compose up

version: "3"
services:
  gui:
    build:
      dockerfile: Dockerfile
    ports:
    - "0.0.0.0:5900:5900"
```

Now run `docker-compose up` to build and run the container.

The last step is to download and run a VNC client. After installing, connect to `localhost` (the default port of 5900 can be used). You should now see a window with the Firefox app running in the Docker environment.

## Resources

* https://en.wikipedia.org/wiki/Virtual_Network_Computing
* https://www.howtogeek.com/devops/how-to-run-gui-applications-in-a-docker-container/
* https://www.realvnc.com/en/connect/download/viewer

[Next >>](040-chapter-04.md)
