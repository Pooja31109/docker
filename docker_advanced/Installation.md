Install docker compose on Linux
```
COMPOSEVERSION=1.27.4
sudo curl -L https://github.com/docker/compose/releases/download/$COMPOSEVERSION/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Test Docker compose version
```
docker-compose version
```
