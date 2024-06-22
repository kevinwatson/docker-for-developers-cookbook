### Chapter 8 - Games

## Introduction

Besides using Docker for tools and background services, computer games are just as portable. The following games are console based. In case you missed it, there's also a few graphical games in [chapter 5](050-chapter-05.md).

### Snake

Snake is an old-school terminal-based game where you use your keyboard to control a snake that eats objects on the screen. Use the keyboard controls below to play.

|Key|Description|
|---|---|
|Up|Go up|
|Down|Go down|
|Left|Go left|
|Right|Go right|
|r|Restart|
|esc|Exit|

To download and play this game, run the docker command below.

```
docker run -ti dyego/snake-game
```

### Tetris

This version of the block-dropping game goes back to its terminal roots. Use the following keyboard controls to play.

|Key|Description|
|---|---|
|Up|Quick drop|
|Down|Slow drop|
|Left|Move left|
|Right|Move right|
|Space|Rotate|
|p|Pause|
|esc|Exit|

To download and run this game, run the command below.

```
docker run -it pdevine/tetromino
```

### Wordle

Wordle is a popular word game in which you try to guess today's five-letter word. There's an open source command line interface (CLI) version that we can download and run.

First, create a directory for the app and move into that directory.

```bash
mkdir ~/wordle-cli-docker
cd ~/wordle-cli-docker
```

Second, add a `Dockerfile`.

```bash
touch Dockerfile
```

Third, copy the following lines into your `Dockerfile` using your favorite text editor.

```
FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y gnupg2 ca-certificates
RUN echo "deb https://deb.nimblebun.works/debian stable main" | tee /etc/apt/sources.list.d/nimblebun.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 033D0D4895F432D1
RUN apt update && apt install -y wordle-cli
ENTRYPOINT ["/usr/games/wordle"]
```

Last, run the commands below to build the image and run the container.

```
docker build -t wordle-cli . && docker run -it wordle-cli
```

## Resources

* https://github.com/DyegoCosta/snake-game
* https://github.com/nimblebun/wordle-cli
* https://hub.docker.com/r/pdevine/tetromino

[Next >>](090-chapter-09.md)
