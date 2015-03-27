## Docker

### Containers
Thanks to LXC technology, containers can now look like full-blown hosts.
Containers can have strong isolation, their own network and storage stacks,
as well as resource management capabilities to allow friendly co-existence
of multiple containers on a host.

### Docker
Docker adds an application deployment engine on top of a virtualized container
execution environment. It is designed to provide a light and fast environment
in which to run your code as well as an efficient workflow to get that code
from your laptop to your test and production environments.

### Core components

#### Docker client and server
Docker is a client-server application. The Docker clients talks to the Docker
server which in turns does all the work.

Docker ships with a command line client binary, docker. This is your client.
Alternatively, you can talk to the Docker server via a RESTful API.

#### Images
Images are the building blocks. You launch your containers from images.
Images are the "build" part of Docker's life cycle.

They are layered-format, Union file systems, built step by step using a set
of instructions.

Images are highly portable and can be shared, stored and updated.

#### Registries
Docker stores the images you build in registries. There are public registries
and private registries.

Docker Inc operates the public registry, Docker Hub, where you can find more
than 10.000 images that people have built and shared. You can of course publish
your images there so that anyone can use them.

You can also setup your own private registry.

#### Containers
Docker helps build and deploy containers inside of which you can package your
applications and services.

Images are the building and packing aspect of Docker while containers are the
running and execution aspect of Docker.

A docker container is an execution environment.

### What can I use Docker for?
* running stand-alone services across multiple environments, a concept specially
useful in SOA or microservices.
* building and testing complex applications locally before deploying to test
and production environments.
* providing lightweight stand-alone sandbox environments for developing, testing
and trying technologies.

### Commands

#### Get info
```
$ sudo docker info

Containers: 0
Images: 25
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 25
Execution Driver: native-0.2
Kernel Version: 3.16.0-31-generic
Operating System: Ubuntu 14.04.2 LTS
CPUs: 8
Total Memory: 15.58 GiB
Name: policarpo
ID: A67L:7GLH:KLFC:QE4Z:CAP2:B7J4:NJMC:HL46:IM3J:6DHH:D4IE:2HBF
WARNING: No swap limit support
```

#### Get help
```
sudo docker help
man docker-run
man docker-attach
man docker-push
man docker-...
```

#### Create a container
```
sudo docker run -it ubuntu /bin/bash
```
We have now created a container that is using the image Ubuntu to run
the command /bin/bash.
The container will run for as long as the process started by the command
/bin/bash runs. Once we kill that process, the container will stop.

The flags -it gives us access to a pseudo-tty so that we can interact
with the process /bin/bash. But if we exit the tty, we kill the process
and the container stops. The container still exists though.

You can give a specific name to your container through the name flag:
```
sudo docker run -it --name great_container ubuntu /bin/bash
```
Naming your containers is really recommended in order to easily identify
your running containers.


#### List running and/or stopped containers
We can show a list of all both stopped and running containers using:
```
sudo docker ps -a
```

To get a list of only the running containers you run:
```
sudo docker ps
```

To get the last container that was run:
```
sudo docker ps -l
```

#### Start a stopped container
```
sudo docker start great_container
```

#### Create a container without running it
```
sudo docker create --name great_container ubuntu /bin/bash
```
Then start it:
```
sudo docker start great_container
```

#### Create daemonized containers
Most containers you run will likely be daemonized. You create a 
daemonized container with the -d flag to tell Docker to detach the
container to the background.
```
sudo docker run -d --name great_container ubuntu /bin/bash -c "while true; do echo Hello world; sleep 1; done")
sudo docker ps
```

#### Stop daemonized container
You can stop a container by sending the SIGTERM signal with:
```
sudo docker stop great_container
```

If you want to be more aggressive, you can issue a SIGKILL signal with:
```
sudo docker kill great_container
```

#### Attach to a running container
```
sudo docker run -d --name great_container ubuntu /bin/bash -c "while true; do echo Hello world; sleep 1; done")
sudo docker ps
sudo docker attach great_container
```

#### Seeing container logs
```
sudo docker logs great_container
sudo docker logs -f great_container
```

#### Inspect processes inside a container
```
sudo docker top great_container
```

#### See CPU / Mem / I/O stats for containers
```
sudo docker stats great_container1 great_container2 great_container3
```

#### Running a new process inside running container
You can run a new process inside a running container with docker exec:
```
sudo docker exec -it great_container /bin/bash
```

You can also run a background process:
```
sudo docker exec -d great_container touch /etc/new_config_file
```


```
```
```
```
```
```
```
```
```
```
```
```
```
```
```
```
```
