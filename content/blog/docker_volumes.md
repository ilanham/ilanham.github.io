---
title: 'Docker Volumes'
date: '2024-04-29T12:12:44-04:00'
draft: false
tags: ['Docker']
---

I think it's hard to overstate how revolutionary Docker has been for the tech industry. A lot of use cases that would have been served by a VM are typically replaced by Docker Containers.  

Good I say - having spent enough time with my elbows deep inside a VM (so to speak), I appreciate the small weight of containers. Unless you're working strictly in the on-premises Microsoft/Windows Server stack, it's the defacto standard for deploying applications.  

Getting started is pretty easy, but diving deeper has many footguns to stumble upon. When you're starting out, I consider data persistence one of those cases. Docker provides options for storing data - I'm going to focus on Docker Volumes.

[Docker Docs - Volumes](https://docs.docker.com/storage/volumes/)

In the link above, I'm focusing on the section [Choose the -v or --mount flag](https://docs.docker.com/storage/volumes/#choose-the--v-or---mount-flag). I've got a couple of commands that show how using `-v` or `--mount` can result in either a bind-mount or a named volume:

### Bind-mount
```bash
docker run --name pg \
    -d \
    -p 5432:5432 \
    -v /Users/ilanham/pgdata:/var/lib/postgresql/data \
    -e POSTGRES_PASSWORD=<secret> \
    postgres
```

The trick above is after the `-v` flag, where I specify a physical file path to the left of the colon. If the path doesn't exist on the filesystem before I try to create this container, Docker will create it.

```bash
docker run --name pg \
    -d \
    -p 5432:5432 \
    --mount type=volume,source=sample,target=/var/lib/postgresql/data \
    -e POSTGRES_PASSWORD=<secret> \
    postgres
```

For the named volume, I'm using the `--mount` syntax, but I can just as easily use `-v`

```bash
docker run --name pg \
    -d \
    -p 5432:5432 \
    -v quick_test:/var/lib/postgresql/data \
    -e POSTGRES_PASSWORD=<secret> \
    postgres
```

### Where are my named volumes?
- Linux: `/var/lib/docker/volumes`
- MacOS: `~/Library/Containers/com.docker.docker/Data/vms/#`[^1]
- Windows: `\\wsl$\docker-desktop-data\data\docker\volumes\<vol_name>`[^2]

[^1]: Docker runs as a virtual machine in MacOS. The volumes are created *inside the VM* as opposed to on the filesystem like a Linux host.
[^2]: When running Docker Desktop on Windows with WSL2, it uses the WSL environment instead of it's own virtual machine. Docker makes a distribution called "docker-desktop-data" which houses all of the volumes you create. The path above let's you access those files without going through the container instance.