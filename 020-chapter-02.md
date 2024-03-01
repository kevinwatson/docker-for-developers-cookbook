### Chapter 2 - Docker Compose

## Introduction

Docker Compose is a feature of Docker which allows you to spin up and interact with a multi-application containerized environment using a single yaml file. While you can use docker commands such as `docker run --rm -it node:latest node` to run the latest node container, if you also wanted to spin up a MySQL database and make calls to the MySQL database from the Node container, you would need to add networking options to both `docker` commands.

In a docker compose file with just a few lines you can define the networking options and both the Node and MySQL images and a single `docker compose up` command will start everything needed for that environment. When should you use a regular `docker` command vs docker compose? I think it comes down to convenience and the environment. If it's a `docker` command you use occasionally and you have memorized the options and image name, using the `docker` command is definitely ok. When there are multiple options that need to be passed like environment variables and remapped ports, etc creating a `compose.yml` file with all of the options preset is easier to manage and running `docker compose up` in those situations is definitely easier to remember.

## Resources

* https://docs.docker.com/compose

[Next >>](030-chapter-03.md)
