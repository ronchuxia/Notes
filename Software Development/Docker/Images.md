# Dockerfile
**Dockerfile** contains instructions for building a Docker image.

```dockerfile
# Pull base image
FROM <repository>

# Set environement variables
ENV <key1>=<value1> \
    <key2>=<value2>

# Run commands
# The default working directory for running these commands is /，unless set otherwise by WORKDIR
RUN <cmd>

# Copy files from the build context into the image
# Use .dockerignore to ignore files
COPY <source> <destination>

# Set working directory
WORKDIR <path>

# Set the main executable to run when the container starts
ENTRYPOINT ["executable", "arg1", "arg2"]

# Set the default arguments for the main executable
# These default arguments can be overridden by the user
CMD ["arg1", "arg2"]
```

Every line of the `Dockerfile` is a **layer**.

# Build Image
```shell
docker build [<options>] <context>
```
Options:
- `-t <name>:<tag>`: Name and tag the image.
- `--progress plain`: Print explicit build output.
- `--no-cache`: Do not use cache, rebuild every layer.

E.g.
```shell
docker build -t myapp:latest .
```

# List Images 
```shell
docker images
```

# Pull Image
```shell
docker pull <name>[:<tag>]
```
- `[:tag]`: optional. Default is `latest`.

# Remove Images
```shell
docker rmi <image> [<image>...]
```

# Tag Image
```shell
docker tag <source-image>[:<tag>] <target-image>[:<tag>]
```

# Push Image
Log in to Docker registry.
```shell
docker login [<server>]
```

Push image to Docker registry.
```shell
docker push <image>[:<tag>]
```
You usually need to tag your image before pushing it to Docker Hub.
```shell
docker tag <image>[:<tag>] <username>/<image>[:tag]
```