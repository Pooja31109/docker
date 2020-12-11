### Setting up a Swamr Cluster

Intialize the first node which willbe our manager
```
docker swarm init --advertise-addr $(curl ifconfig.me)
```
a new node can be added to the cluster only if it contains the token generated when Swarm was initialized.
Copy the the command from above output to add a new node to cluster
```
docker swarm join --token <token> <swarm manager ip>:2377
```

go to node 2, paste the command from above
do it ditto in other nodes

in any case, u forgot manager token, worker token
```
docker swarm join-token -q worker
docker swarm join-token -q manager
```

verify the cluster
```
docker node ls
```
