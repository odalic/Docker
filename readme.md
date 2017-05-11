# Odalic Docker
Docker for hosting Odalic server and UI v1.1

## Docker setup
You can find Docker for all major platforms [here](https://www.docker.com/community-edition).

Please note, that Docker requires Hyper-V on Windows, so it cannot be installed on Windows 10 Home.

## Useful Docker commands

Please navigate to the dockerfile in your Docker console. You can build the Docker image by executing:

```
docker build --tag odalic:latest .
```

The following Docker command can run the built Docker image:

```
docker run -ti --name odalic -p 8080:8080 odalic:latest
```

If you want to access the odalic installation files and configuration, you must run the odalic image in the detached mode:

```
docker run -d --name odalic -p 8080:8080 odalic:latest
```

You can then start Linux command line by executing:

```
docker exec -ti odalic sh
```

Starting a Docker image will create a Docker container. You can start/stop the created container like this:

```
docker start/stop odalic
```

For mode advanced command please refer to the [Docker documentation](https://docs.docker.com/engine/reference/commandline/cli/).