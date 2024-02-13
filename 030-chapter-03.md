### Chapter 3 - Console

## Introduction

Sometimes you need to test a command or script in a specific environment. Docker makes it easy to download and run a temporary environment (or specific version of an environment) without the need to install and later uninstall an environment.

Each docker command below uses the `latest` tag. This tag can be replaced with a more specific label or version which makes it easy to spin up a specific container and run them side by side in separate terminal windows.

### Options

```bash
--rm # remove the container when it is stopped to save hard drive space
-it # an interactive terminal session allows you to interact with the container
```

## Programming Languages

### Node/JavaScript

```bash
docker run --rm -it node:latest node
```

### Python

```bash
docker run --rm -it python:latest python
```

### Ruby

```bash
docker run --rm -it ruby:latest irb
```

## Operating Systems

Spinning up a pre-configured operating system in a Docker container when you already have the Docker environment installed is a much faster way to experiment with an environment than installing and maintaining separate virtual machine.

### Alpine Linux

```bash
docker run --rm -it alpine:latest sh
```

### Ubuntu

```bash
docker run --rm -it ubuntu:latest bash
```

## Resources

* https://hub.docker.com/_/alpine
* https://hub.docker.com/_/node
* https://hub.docker.com/_/python
* https://hub.docker.com/_/ruby
* https://hub.docker.com/_/ubuntu

[Next >>](040-chapter-04.md)
