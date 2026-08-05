### Chapter 2 - Apple Container

## Introduction

Apple Container is an official project backed by Apple for macOS. It runs on macOS Tahoe (v26) and up on Apple Silicon ARM processors (M1 and higher). It allows you to run build and run containers without installing Docker Engine or Docker Desktop.

## Example

We can install Apple Container by downloading and running the installer found here: https://github.com/apple/container/releases. Once it's installed, run this command to start the service in a terminal:

```bash
% container system start

Launching container-apiserver...
Testing access to container-apiserver...
Verifying machine API server is running...
```

Now let's run a container. Notice that the command is similar to a docker command, but substituting the `docker` with the `container` command.

```bash
% container run --rm -it ubuntu:latest bash
root@f5677c39-149c-4afa-8dcb-8562978d1787:/# whoami
root
root@f5677c39-149c-4afa-8dcb-8562978d1787:/# uname -a
Linux f5677c39-149c-4afa-8dcb-8562978d1787 6.18.15 #1 SMP Tue Mar 17 01:36:53 UTC 2026 aarch64 GNU/Linux
```

We can list running containers

```bash
% container list --all
ID                                    IMAGE                            OS     ARCH   STATE    IP               CPUS  MEMORY   STARTED
a4cc9cf4-3832-4713-901f-d7451f9d995e  docker.io/library/ubuntu:latest  linux  arm64  running  192.168.64.3/24  4     1024 MB  2026-08-05T08:07:17Z
```

Apple Container can also read Dockerfiles and build containers:

```dockerfile
FROM ubuntu:latest
RUN apt update && apt install sqlite3 -y
```

Build it

```bash
% container build --tag sqlite3-test --file Dockerfile .

[+] Building 9.7s (6/6) FINISHED
 => [resolver] fetching image...docker.io/library/ubuntu:latest 0.0s
...
 => => sending tarball                                          0.5s
sqlite3-test:latest
```

Run it

```bash
% container run --rm -it sqlite3-test bash

root@aa5b7777-19ec-44f7-a4e1-3e31d32ad718:/# sqlite3
SQLite version 3.46.1 2024-08-13 09:16:08
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite>
```

## References

* https://github.com/apple/container/tree/main
* https://github.com/apple/container/blob/main/docs/tutorials/start-here.md

[Next >>](030-chapter-03.md)
