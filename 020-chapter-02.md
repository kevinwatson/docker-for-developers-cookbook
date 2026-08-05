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

Now let's run a container. Notice that the command is similar to a docker command, but substituting the `docker` with the `container` command:

```bash
% container run --rm -it ubuntu:latest bash
root@f5677c39-149c-4afa-8dcb-8562978d1787:/# whoami
root
root@f5677c39-149c-4afa-8dcb-8562978d1787:/# uname -a
Linux f5677c39-149c-4afa-8dcb-8562978d1787 6.18.15 #1 SMP Tue Mar 17 01:36:53 UTC 2026 aarch64 GNU/Linux
```

## References

* https://github.com/apple/container/tree/main
* https://github.com/apple/container/blob/main/docs/tutorials/start-here.md

[Next >>](030-chapter-03.md)
