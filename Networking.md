### Networking
we are going to take a look at the basics of Docker networking and Docker volumes using the default drivers. Let's take a look at networking examples first.

Before we launch our application, let's download the container images we will be using, and also create the network:
```
docker image pull redis:alpine
docker image pull russmckendrick/moby-counter
docker network create moby-counter
```
Now that we have our images pulled and our network created, we can launch our containers, starting with the Redis one:
```
docker container run -d --name redis --network moby-counter redis:alpine
```
Now that the Redis container is launched, we can launch the application container by running the following command:
```
docker container run -d --name moby-counter --network moby-counter -p 8080:80 russmckendrick/moby-counter
```
All that remains now is to access the application. To do this, open your browser and go to http://localhost:8080/. You should be greeted by a mostly blank page, with the message Click to add logos…

Let's try using the exec command to ping the redis container from the moby-counter application and see what we get:
```
docker container exec moby-counter ping -c 3 redis
```
You may be thinking that the application's host file contains an entry for the redis container; let's take a look using the following command:
```
docker container exec moby-counter cat /etc/hosts
```
let's check /etc/resolv.conf by running the following command:
```
docker container exec moby-counter cat /etc/resolv.conf
```
Let's create a second network and launch another application container:
```
docker network create moby-counter2
docker run -itd --name moby-counter2 --network moby-counter2 -p 9090:80 russmckendrick/moby-counter
```
Now that we have the second application container up and running, let's try pinging the redis container from it:
```
docker container exec moby-counter2 ping -c 3 redis
#it gives you an error
```
Let's check the resolv.conf file to see whether the same nameserver is being used already, as follows:
```
docker container exec moby-counter2 cat /etc/resolv.conf
```

As we have launched the moby-counter2 container in a different network to that where the container named redis is running, we cannot resolve the hostname of the container:
```
docker container exec moby-counter2 nslookup redis 127.0.0.11
```
Let's look at launching a second Redis server in our second network.
```
docker container run -d --name redis2 --network moby-counter2 --network-alias redis redis:alpine
docker container exec moby-counter2 nslookup redis 127.0.0.1
```
You can find out more information about the configuration of the networks by running the following inspect command:
```
docker network inspect moby-counter
```
Before we progress to learn docker volumes, we should remove one of the applications and associated networks. To do this, run the following commands:
```
docker container stop moby-counter2 redis2
docker container prune
docker network prune
```
