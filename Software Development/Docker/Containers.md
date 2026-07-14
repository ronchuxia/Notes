# Create Container
```shell
docker run [<options>] <image> [<command>] [<args>...]
```

E.g.
```bash
docker run \
	-it \
	-v <host-path>:<container-path> \
	--name <container_name> \
	<image>
```
Options:
- `-i`: Keep STDIN open.
- `-t`: Allocate a pseudo-terminal.
- `-v`: Mount a volume.
- `--name`: Name the container.

STDIN (Standard Input) is the "input pipe" for a program. In a normal terminal, your keyboard is connected to this pipe. When you type, you are sending those characters through STDIN to the shell. `-i` keeps STDIN open.

Most Linux programs behave differently depending on whether they are talking to a human or another program. `-t` asks Docker to "fake" a terminal so that the software inside the container thinks it's talking to a real human at a keyboard.

E.g.
```shell
docker run -d <image>
```
Options:
- `-d`: **Detached mode.** Run the containers in the background.

# List Containers
```bash
docker ps [<options>]
```
Options:
- `-a`: List all containers, including stopped containers.

# Start and Stop Container
```bash
docker start <container>
docker stop <container>
docker kill <container>
```

The volume mount configured when the container was created is automatically restored when the container is started again.

# Run Command in Container
`docker exec` runs a new command in an already running container. 
```bash 
docker exec [<options>] <container> <command> [<args>...]
```

E.g.
Enter the running container and start an interactive bash shell.
```shell
docker exec -it my-container bash
```

# Copy File From/To Container
Copy from host to container.
```shell
docker cp <source> <container>:<destination>
```

Copy from container to host.
```shell
docker cp <container>:<source> <destination>
```

# Remove Container
```bash
docker rm <container>
```