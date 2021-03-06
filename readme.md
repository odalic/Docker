# Odalic Docker
Docker for hosting Odalic server and UI v1.1

## Docker setup
You can find the Docker installation files for all major platforms here: [https://www.docker.com/community-edition](https://www.docker.com/community-edition).

Please note, that Docker for Windows requires Hyper-V, so it cannot run natively on Windows 10 Home or older Windows versions. You have to use the Docker Tools instead: [https://www.docker.com/products/docker-toolbox](https://www.docker.com/products/docker-toolbox).

## Running Odalic

Odalic requires a working SPARQL endpoint with update rights. An easy way to setup such endpoint is to run the virtuoso Docker image:

```
docker run --name localKB -p 8890:8890 -e SPARQL_UPDATE=true -e DEFAULT_GRAPH=http://odalic.eu -d tenforce/virtuoso
```

To build the Odalic Docker image, execute:    

```
docker build --tag odalic:latest https://github.com/odalic/odalic-docker.git
```

If you do not have git, you have to download the dockerfile and run:

```
docker build --tag odalic:latest .
```

The following Docker command will run the prepared Docker image:

```
docker run -ti --name odalic --link localKB -p 8080:8080 odalic:latest
```

The Odalic UI can be now accessed from your favourite browser on [localhost:8080/odalic-ui](http://localhost:8080/odalic-ui).

## Accessing the virtual machine

If you want to access the odalic installation files and configuration, you have to run the Odalic image in a detached mode:

```
docker run -d --name odalic --link localKB -p 8080:8080 odalic:latest
```

You can then start the Linux command line by executing:

```
docker exec -ti odalic sh
```

## Changing ports

You can generally change a docker container port by changing the "-p" parameter:

```
-p 8080:[your local port]
```

You can freely change the local SPARQL endpoint port. It is only used when you access it directly over: [http://localhost:8890/sparql](http://localhost:8890/sparql).

To change the Odalic port, you have to access the Odalic virtual machine and edit following files:

```
/usr/local/tomcat/webapps/odalic-ui/config.txt
/usr/local/odalic/config/sti.properties
```

For more information please consult the Odalic documentation: [https://github.com/odalic/sti/releases/download/v1.1.1/ODALIC.Project.Documentation.pdf](https://github.com/odalic/sti/releases/download/v1.1.1/ODALIC.Project.Documentation.pdf).

## Starting and stopping the Odalic container

Running a Docker image will create a Docker container. You can start/stop the created container like this:

```
docker start odalic
docker stop odalic
```

## Updating Odalic

If you want to update your Docker container to a new Odalic version, you have to first stop the existing container. Then remove it by executing:

```
docker container rm -f odalic
```

After the container is removed, you can update the image by running the build again:

```
docker build --tag odalic:latest https://github.com/odalic/odalic-docker.git
```

# Advanced Docker configuration

For more advanced commands please refer to the Docker documentation [https://docs.docker.com/engine/reference/commandline/cli](https://docs.docker.com/engine/reference/commandline/cli).
