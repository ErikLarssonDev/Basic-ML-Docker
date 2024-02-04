# Basic-ML-Docker
A basic docker setup for ML

### Step 1: Install Docker

If you don't have Docker installed, follow the links below to install Docker for your system:
- [Install Docker Engine](https://docs.docker.com/engine/install/)

### Step 2: Install Nvidia Container Toolkit (Optional)
If you plan to use GPU acceleration with CUDA, install Nvidia Container Toolkit:

- [Nvidia Container Toolkit Installation Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

### Step 3: Build the Docker Image
Navigate to the directory containing the Dockerfile and build the Docker image with:

```bash
docker build -t example-image .
```

### Step 4: Run the Docker Container in Detached Mode
Run the following command to start the container in detached mode:

```bash
docker run -d \
  --gpus all \
  -v "${PWD}:/code" \
  -p 8080:8080 \
  --name "example-container" \
  --env AUTHENTICATE_VIA_JUPYTER="mytoken" \
  example-image \
  tail -f /dev/null
```

This will start a new Docker container named `example-container` that will not exit immediately. The `-d` flag runs the container in detached mode, letting it run in the background.

### Step 5: Interact with the Docker Container
To attach an interactive shell to the running container, use the command:

```bash
docker exec -it example-container /bin/bash
```

You can now interact with your container using the bash shell.

### Additional Notes
- If you wish to stop the container, you can do so with `docker stop example-container`.
- To start the container again after stopping, use `docker start example-container`.
- In case you need to remove the container, make sure it's stopped and then run `docker rm example-container`.
- To see the output from the container (logs), use `docker logs example-container`.
