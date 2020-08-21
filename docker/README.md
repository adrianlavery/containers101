# Docker demo script

## Create an image
```
docker build -t ubuntu:Apache_Server .
```

## List the images
```
docker images | grep -i Apache_Server
```

## Create a container from the image
```
docker run --name Apache_Instance -p 3000:80 -d ubuntu:Apache_Server
```

## Check if the container is running
```
docker ps
```

# Verify we can browse to the web server
```
http:/localhost:3000
```
> **Note** if you are using codespaces, ports 3000 and 3001 are forwarded via devcontainer.json