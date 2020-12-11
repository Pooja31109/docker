### Portainer
```
docker image pull portainer/portainer
docker volume create portainer_data
docker container run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

browse with your `<Public IP>:9000`

