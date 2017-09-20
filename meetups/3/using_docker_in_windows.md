# Playing with Docker in Windows using docker-machine

This readme file aims to describe how one can use docker-machine to play around with Docker through their Windows environment,
without the need for creating a Virtual Machine.

## Installation

You can get docker-machine for Windows by navigating to the following URL: https://www.docker.com/products/docker-toolbox
During the installation process, make sure you check the following:

- VirtualBox if you don't already have Virtualbox installed on your machine
- Docker Compose
- Git for Windows in case you want to version your code / files and in case you don't have it already installed

## Using
In order to use the Docker machine, you just have to open the "Docker Quickstart Terminal" application. It provides a shell and piggybacks on Virtualbox, creating a
headless Virtual Machine with Docker installed under the hood. Don't worry, you can manage Docker like it's installed natively on Windows by using the docker machine terminal.

### Examples

*Creating a container*

Let's start by creating a new container: `docker run -itd alpine test /bin/sh
Something like the following will appear in the screen:

```
$ docker run -itd alpine test /bin/sh
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
88286f41530e: Pull complete
Digest: sha256:f006ecbb824d87947d0b51ab8488634bf69fe4094959d935c0c103f4820a417d
Status: Downloaded newer image for alpine:latest
619ecbe2da43560833a19e782bbca73697e427ee5864ce1ad73cf4b27fd57c2b
```

What we have done with that command is the following:
1. Fetch the alpine image and store it locally
2. Use the alpine image to spin up a new container named 'test'
3. Execute the 'sh' shell as the new container's main process

We have created the new container in detached mode, i.e. we are in our initial shell, not in the container shell. To attach the container, run:
`docker attach test` and press Enter a couple of times. In order to detach from the container shell, press `Ctrl+P, Ctrl+Q`.

In general, you can issue any command you want, just like if Docker was installed natively. The only difference is that the commands are sent in the VM by Docker Machine.
The only exception here is when you want to share data with the host (i.e. mount a host volume to the docker container). See the "Attaching a volume" section below for that.

*Creating an image*

This holds true for cases when you want to copy your files in the container (e.g. when building an image using a Dockerfile). Let's say you have the following in your Dockerfile:

```
FROM alpine
ADD notes.txt /notes.txt
CMD ["/bin/sh"]
```

And you have a notes.txt file in the same directory as your Dockerfile, you can go into this directory and use the following command to build a new image from that Dockerfile:
`docker build -t my_new_image .`

After creating the image, you can spin up a new container, attach to its shell and validate the existence of the notes.txt file

*Attaching a volume*

In order to attach a host directory in a container, this directory has to exist in the Docker host, which is the VM that Docker Machine has created for you. This is very easy, 
as you can use the Docker Machine terminal to connect to the VM by issuing the following command:
`docker-machine ssh`

Please note that an error like the following may occur: `dial-http tcp 127.0.0.1:55527: read tcp 127.0.0.1:55528->127.0.0.1:55527: wsarecv: An existing connection was forcibly closed by the remote host.`,
but if you issue the command again, you will be provided a shell to the Virtual Machine.

What you have to do next is create the directory that you want to mount to the new container, along with any files in it. For our example, we have created a `my_dir` directory in `/home/docker/` of the VM,
which contains a `my_file` file with some content in it. To create a container that has this directory mounted, we have to do:
`docker run -itd -v /home/docker/my_dir:/my_dir <image_name> /bin/sh`

The *full* path of the VM directory has to be provided. You can validate that the directory has been successfully mounted, by attaching to the container and navigating to it.
