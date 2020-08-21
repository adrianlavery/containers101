# Docker networking demo script

---
**NOTE**

This demo script is dependent on the [docker demo running](../DEMO.md) running

---

## List networks

```
docker network ls
```

## Check the Apache container is on the bridge network and get it's IP address

```
docker network inspect bridge
```

## Pull the curl image and run curl against the Apache container

```
docker run --rm -it curlimages/curl:latest 172.17.0.2
docker run --rm -it curlimages/curl:latest Apache_Instance
```
> **Note** the curl command fails against the name of the container

## Create a user defined bridge network

```
docker network create containers101
```

## Run a new apache container on the containers101 network

```
docker run --name Apache_Instance2 --network=containers101 -p 3001:80 -d ubuntu:Apache_Server
```

## Check the new Apache container is on the containers101 network and get it's IP address

```
docker network inspect containers101
```

## Pull the curl image and run curl against the new Apache container

```
docker run --rm -it --network=containers101 curlimages/curl:latest 172.18.0.2
docker run --rm -it --network=containers101 curlimages/curl:latest Apache_Instance2
```
> **Note** this time the curl command works against the name of the container