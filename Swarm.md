### Deploying services to the Swarm cluster
Before we deploy a demo service, we should create a new network so that all containers that constitute the service can communicate with each other no matter on which nodes they are deployed:
```
docker network create --driver overlay go-demo
```
We can check the status of all networks with the command that follows:
```
docker network ls
```
The go-demo application requires two containers. Data will be stored in MongoDB. The back-end that uses that DB is defined as vfarcic/go-demo container.

Let's start by deploying the mongo container somewhere within the cluster.
Usually, we'd use constraints to specify the requirements for the container (example: HD type, the amount of memory and CPU, and so on). We'll skip that, for now, and tell Swarm to deploy it anywhere within the cluster:
```
docker service create --name go-demo-db --network go-demo mongo:3.2.10
```
Please note that we haven't specified the port Mongo listens to 27017. That means that the database will not be accesible to anyone but other services that belong to the same go-demo network.

As you can see, the way we use service create is similar to the Docker run command you are, probably, already used to.

We can list all the running services:
```
docker service ls
```
Depending on how much time passed between service create and service ls commands, you'll see the value of the REPLICAS column being zero or one. Immediately after creating the service, the value should be 0/1, meaning that zero replicas are running, and the objective is to have one. Once the mongo image is pulled, and the container is running, the value should change to 1/1.

If we need more information about the go-demo-db service, we can run the service inspect command:
```
docker service inspect go-demo-db
```
Now that the database is running, we can deploy the go-demo container:
```
docker service create --name go-demo -e DB=go-demo-db --network go-demo vfarcic/go-demo:1.0
```
There's nothing new about that command. The service will be attached to the go-demo network. The environment variable DB is an internal requirement of the go-demo service that tells the code the address of the database.

At this point, we have two containers (mongo and go-demo) running inside the cluster and communicating with each other through the go-demo network. Please note that none of them is yet accessible from outside the network. At this point, your users do not have access to the service API. you need a reverse proxy capable of utilizing the new Swarm networking to access ur service API ( setting up reverse proxy the beyond the scope of this class)

Let's run the service ls command one more time:
```
docker service ls
```
#### What happens if we want to scale one of the containers? How do we scale our services?

We should always run at least two instances of any given service. That way they can share the load and, if one of them fails, there will be no downtime. 
We can, for example, tell Swarm that we want to run five replicas of then go-demo service:
```
docker service scale go-demo=5
```
With the service scale command, we scheduled five replicas. Swarm will make sure that five instances of go-demo are running somewhere inside the cluster.

We can confirm that, indeed, five replicas are running through the, already familiar, service ls command:
```
docker service ls
```
As we can see, five out of five REPLICAS of the go-demo service are running.

The service ps command provides more detailed information about a single service:
```
docker service ps go-demo
```
We can see that the go-demo service is running five instances distributed across the three nodes. Since they all belong to the same go-demo SDN, they can communicate with each other no matter where they run inside the cluster. At the same time, none of them is accessible from outside:

#### What happens if one of the containers is stopped or if the entire node fails? 
After all, processes and nodes do fail sooner or later. Nothing is perfect, and we need to be prepared for such situations.
* shutdown any one of workers
* Check your services with `docker service ls`
* check your nodes with `docker node ls`

