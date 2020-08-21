# Docker storage demo script


## Container filesystem

Create an alpine container and start an interactive shell 
```
docker run -it alpine /bin/ash
``` 

Write a file to the container filesystem via the interactive shell
```
echo "`hostname`  `date`" > demo.log
```
Read the file 
```
cat demo.log
# Exit the container session
exit
``` 
Remove the container and create new container

```
# Get the id of the container to delete
docker ps -a
# Remove the container
docker rm -f ad49430522e2
# Create a new version of the container
docker run -it alpine /bin/ash
```
Is the file there? 
```
cat demo.log
```


## Docker volumes

Create a new volume
```
docker volume create demo
```
List the existing volumes
```
docker volume ls
```
Create a container and attach the volume
```
docker run -v demo:/containers101 -it alpine /bin/ash
```
Write a file to the container filesystem via the interactive shell
```
echo "`hostname`  `date`" > /containers101/demo.log
```
Read the file 
```
cat /containers101/demo.log
# Exit the container session
exit
``` 
Remove the container and create new container

```
# Get the id of the container to delete
docker ps -a
# Remove the container
docker rm -f ad49430522e2
# Create a new version of the container
docker run -v demo:/containers101 -it alpine /bin/ash
```
Write a file to the container filesystem via the interactive shell
```
echo "`hostname`  `date`" >> /containers101/demo.log
```
Read the file and notice that the new container hostname has been appended
```
cat /containers101/demo.log
``` 
Create another container in a separate terminal using the same volume
```
docker run -v demo:/containers101 -it alpine /bin/ash
```
Write a file to the container filesystem via the interactive shell
```
echo "`hostname`  `date`" >> /containers101/demo.log
```
Read the file and notice that the new container hostname has been appended and both running containers can access the same volume
```
cat /containers101/demo.log
``` 
