### Chapter 8 - Games

## Introduction

Besides using Docker for tools and background services, computer games are just as portable. Some of the following games are console based while others utilize a graphical user interface.

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

### GNOME Mines

GNOME Mines is a Linux-based clone of an old school puzzle game named Minesweeper that came installed on early versions of Microsoft Windows. With Docker, we can run the Linux versions anywhere. The objective is to click on the squares on the grid without exposing the mines.

First, create a directory for the app and move into that directory.

```bash
mkdir ~/gnome-mines-docker
cd ~/gnome-mines-docker
```

Second, add a `Dockerfile`.

```bash
touch Dockerfile
```

Third, copy the following lines into your `Dockerfile` using your favorite text editor.

```
FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y x11vnc xvfb gnome-mines
RUN echo "exec ./usr/games/gnome-mines" > ~/.xinitrc && chmod +x ~/.xinitrc
CMD ["/usr/bin/x11vnc", "-create", "-forever"]
```

Fourth, add a `docker-compose.yml` file to the same directory and copy the contents below into this file.

```
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

Fifth, run `docker-compose up` to build and run the container.

Lastly, using your VNC client (you can download the viewer [here](https://www.realvnc.com/en/connect/download/viewer)), connect to `localhost`. The client should default to port `5900` which is defined in the `docker-compose.yml` file above. After a few seconds you should see a window with the Minesweeper clone running in the Docker environment. Enjoy!

### Crack Attack!

Crack Attack! is a clone of a Super Nintendo game named Tetris Attack. The objective is to eliminate the blocks by lining up similar colors and before you run out of time.

First, create a directory for the app and move into that directory.

```bash
mkdir ~/crack-attack-docker
cd ~/crack-attack-docker
```

Second, add a `Dockerfile`.

```bash
touch Dockerfile
```

Third, copy the following lines into your `Dockerfile` using your favorite text editor.

```
FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y x11vnc xvfb crack-attack
RUN echo "exec ./usr/games/crack-attack" > ~/.xinitrc && chmod +x ~/.xinitrc
CMD ["/usr/bin/x11vnc", "-create", "-forever"]
```

Fourth, add a `docker-compose.yml` file to the same directory and copy the contents below into this file.

```
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

Fifth, run `docker-compose up` to build and run the container.

Lastly, using your VNC client, connect to `localhost`. The client should default to port `5900` which is defined in the `docker-compose.yml` file above. After a few seconds you should see a window with the Crack Attack! running in the Docker environment. Game play and controls can be found on the author's website here: https://aluminumangel.org/attack/#game%20play

### GNOME Sudoku

Sudoku is the GNOME version of the Japanese logic game with the same name. The objective is to fill the empty cells with a number between 1 and 9 so that no number is repeated on a row, column or 3x3 box.

First, create a directory for the app and move into that directory.

```bash
mkdir ~/gnome-sudoku-docker
cd ~/gnome-sudoku-docker
```

Second, add a `Dockerfile`.

```bash
touch Dockerfile
```

Third, copy the following lines into your `Dockerfile` using your favorite text editor.

```
FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y x11vnc xvfb gnome-sudoku
RUN echo "exec ./usr/games/gnome-sudoku" > ~/.xinitrc && chmod +x ~/.xinitrc
CMD ["/usr/bin/x11vnc", "-create", "-forever"]
```

Fourth, add a `docker-compose.yml` file to the same directory and copy the contents below into this file.

```
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

Note: As an alternative to the docker-compose.yml file above, you can run the following docker commands:

```
docker build -t gnome-sudoku . && docker run -p "0.0.0.0:5900:5900" gnome-sudoku
```

Fifth, run `docker-compose up` to build and run the container.

Lastly, using your VNC client, connect to `localhost`. The client should default to port `5900` which is defined in the `docker-compose.yml` file above. After a few seconds you should see a window with the GNOME Sudoku running in the Docker environment. Game play and controls can be found here: https://wiki.gnome.org/Apps/Sudoku

## Resources

* https://aluminumangel.org/attack/
* https://en.wikipedia.org/wiki/Virtual_Network_Computing
* https://github.com/DyegoCosta/snake-game
* https://github.com/nimblebun/wordle-cli
* https://help.gnome.org/users/gnome-mines/stable/
* https://www.howtogeek.com/devops/how-to-run-gui-applications-in-a-docker-container/
* https://hub.docker.com/r/pdevine/tetromino
* https://wiki.gnome.org/Apps/Sudoku
* https://www.realvnc.com/en/connect/download/viewer

[Next >>](090-chapter-09.md)
