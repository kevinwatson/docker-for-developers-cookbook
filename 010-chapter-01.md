### Chapter 1 - Docker

## Introduction

Docker is a tool that uses Linux namespaces to isolate processes into containers. Packaging processing into containers provides many benefits, including creating portable, self-contained applications and maximizing hardware utilization. Docker is a company which provides tooling for a wide array of operating systems, including Microsoft Windows and MacOS and Linux.

## Maintenance

Just because Docker makes applications portable, that doesn't mean that they are minimal. Docker images can often include unused toolsets and operating system features that can take up a lot of additional hard drive space. Just like Docker makes it easy to download and run an app, it's also easy to remove the app and its related images.

Viewing and deleting images is as simple as running the following commands.

Show the images, their tags, ids and sizes.

```
docker images
```

Scan through the list for the specific image you want to remove. Once you find the `image id`, run this next command.

```
docker image rm [paste image id here]
```

If you see an error like `Error response from daemon: conflict: unable to delete 4811999c98af (must be forced) - image is being used by stopped container e7517b7f9afe`, it means that at one point there was a running container based on that image and the image cannot be deleted. Run this command to removed the container files.

```
docker container rm [paste container id here]
```

If it was successful, you'll see the `container id` from the command printed on the next line. You can then run the `docker image rm [image id]` command again. This time you'll see lines like the following.

```
Deleted: sha256:190764016d9ed33f2492fe6df1846255ca17bc54984219329cf7b2924d1ff957
Deleted: sha256:6fc9c0a80ea0dcd8a0ab0fb0e2ea6a2f198a23cb4331903492f15ded1bc23166
```

If you would rather not spend time picking through and making decisions on which Docker images need to be deleted and just need to free up some hard drive space, you can use the `prune` command below to easily remove unused images.

```
docker image prune --all
```

## Docker Compose

Docker Compose is a feature of Docker which allows you to spin up and interact with a multi-application containerized environment using a single yaml file. While you can use docker commands such as `docker run --rm -it node:latest node` to run the latest node container, if you also wanted to spin up a MySQL database and make calls to the MySQL database from the Node container, you would need to add networking options to both `docker` commands.

In a docker compose file with just a few lines you can define the networking options and both the Node and MySQL images and a single `docker compose up` command will start everything needed for that environment. When should you use a regular `docker` command vs docker compose? I think it comes down to convenience and the environment. If it's a `docker` command you use occasionally and you have memorized the options and image name, using the `docker` command is definitely ok. When there are multiple options that need to be passed like environment variables and remapped ports, etc creating a `compose.yml` file with all of the options preset is easier to manage and running `docker compose up` in those situations is definitely easier to remember.

## Resources

* https://docs.docker.com/compose
* https://docs.docker.com/reference/cli/docker/image/
* https://www.docker.com
* https://en.wikipedia.org/wiki/Linux_namespaces

[Next >>](020-chapter-02.md)
