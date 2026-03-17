# Commonly used Docker CLI commands

## Docker containers & images

```bash
# list running containers
docker ps

# list all containers
docker ps -a 

# Downloads a Docker image from Docker Hub
docker pull [image name]:[tag] 

# Lists all Docker images that you have locally
docker images 

# run a Docker container from a Docker image.
docker run [image name | image id]:[tag] 

# runs in detached mode, doesn't hijack your terminal
docker run -d [image name | image id]:[tag] 

# port binding
docker run -d -p [local port]:[container port] [image name | image id]:[tag]

# name the container
docker run --name [given name] -d -p [local port]:[container port] [image name]:[tag]

# Fetches the logs of a container.
docker logs [container name | container id]

# Stops a running Docker container.
docker stop [container name | container id]

# starts an existing container
docker start [container name | container id]

# Deletes a Docker container.
docker rm [container name | container id]

# Removes a Docker image.
docker rmi [container name | container id]
```

## DOCKER FILE

The file from which an image is built

### FROM

Sets the base image for subsequent instructions.
A valid Dockerfile must start with a `FROM` instruction.
Example: `FROM ubuntu:18.04`

### COPY

Copies files or directories from `<src>`
and adds them to the filesystem of the container at the path `<dest>`
Example: `COPY . /app/`
the trailing slask `/` means create this folder if it doesn't exist
Example: `COPY package.json /app/`
Example: `COPY src /app/`

### WORKDIR

Sets the working directory
for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` and `ADD` instructions that follow it in the Dockerfile.
Example: `WORKDIR /app`

### RUN

Executes any commands in a shell/terminal inside the container environment
The commands add a new layer on top of the current image and commit the results.
The resulting committed image will be used for the next step in the Dockerfile.
Example: `RUN npm install`
Example: `RUN apt-get update && apt-get install -y python3`

### CMD

Provides defaults for an executing container.
These can include an executable, or they can omit the executable, in which case you must specify an `ENTRYPOINT` command.
Example: `CMD ["executable","param1","param2"]`
Example: `CMD ["node","server.js"]`

### ENTRYPOINT

This command allows you to configure a container that will run as an executable.
Example: `ENTRYPOINT ["executable", "param1", "param2"]`

### ADD

This command copies new files, directories or remote file URLs from `<src>` and adds them to the filesystem of the container at the path `<dest>`. `ADD` has some features (like local-only tar extraction and remote URL support) not present in `COPY`.
Example: `ADD . /app`

### EXPOSE

This command informs Docker that the container listens on the specified network ports at runtime.
Example: `EXPOSE 8080`

### ENV

This command sets the environment variable `<key>` to the value `<value>`. This value will be in the environment for all subsequent instructions in the build stage and can be replaced inline in many as well.
Example: `ENV MY_NAME="John Doe"`

### VOLUME

This command creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.
Example: `VOLUME /myvol`

### ARG

This command defines a variable that users can pass at build-time to the builder with the `docker build` command.
Example: `ARG VERSION=latest`

### USER

This command sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any `RUN`, `CMD` and `ENTRYPOINT` instructions that follow it in the Dockerfile.
Example: `USER myuser`

Remember, the order of commands in a Dockerfile matters because each command in a Dockerfile results in a new image layer. Later commands can use the results of previous commands. Also, Docker uses a build cache – if a particular command has been executed before and nothing has changed, Docker uses the cached result, which can make building images faster.

## Build a DOCKER IMAGE from a DOCKER FILE

`docker build -t [name:tag] .`
Builds a Docker image from a Dockerfile in the current directory.
The `-t` option lets you specify a name and tag for the image.

`docker exec -it [container_id]`
Runs a command in a running container.
The `-it` options make the session interactive so you can interact with the command.
You can specify the container either by its name or ID.

## Docker Compose

`docker-compose up`
Starts all services defined in a `docker-compose.yml` file

`docker-compose down`
Stops and removes all services defined in a `docker-compose.yml` file.

### Help

`docker --help`

`docker [command] --help`
