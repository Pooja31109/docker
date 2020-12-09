### Volumes
When you go to the application in a browser (at http://localhost:8080/), you will probably see that there already are Docker logos on screen. Let's stop and then remove the Redis container and see what happens. To do this, run the following commands:
```
docker container stop redis
docker container rm redis
```
If you have your browser open, you may notice that the Docker icons have faded into the background and there is an animated loader in the center of the screen. This is basically to show that the application is waiting for the connection to the Redis container to be re-established, Relaunch the Redis container using the following command:
```
docker container run -d --name redis --network moby-counter redis:alpine
```
Once you have a pattern, let's remove the Redis container again by running the following commands:
```
docker container stop redis
docker container rm redis
```
losing the data in the container is to be expected. However, as we used the official Redis image, we haven't, in fact, lost any of our data.
The Dockerfile for the official Redis image that we used available in dockerhub, lets review it: https://hub.docker.com/_/redis

If you notice, during the last part of the file, there are the VOLUME and WORKDIR directives declared; this means that when our container was launched, Docker actually created a volume and then run redis-server from within the volume. We can see this by running the following command:
```
docker volume ls
```

run the following command, making sure you replace the volume ID with that of your own:
```
docker container run -d --name redis -v 45c4cb295fc831c085c49963a01f8e0f79534b9 f0190af89321efec97b9d051f:/data -network moby-counter redis:alpine
```
You can view the contents of the volume by running the following command to attach the container and list the files in /data:
```
docker container exec redis ls -lhat /data
```

you can override the volume with your own. To create a volume, we need to use the volume command:
```
docker volume create redis_data
docker container run -d --name redis -v redis_data:/data --network moby-counter redis:alpine
```

Like the network command, we can view more information on the volume using the inspect command, as follows:
```
docker volume inspect redis_data
```
