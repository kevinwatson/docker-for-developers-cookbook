### Chapter 8 - Games

## Introduction

Besides using Docker for tools and background services, computer games are just as portable.

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


```
docker run -it pdevine/tetromino
```

## Resources

* https://github.com/DyegoCosta/snake-game

[Next >>](080-chapter-08.md)
