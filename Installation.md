### Install docker on Linux
```
sudo yum install vim tree git docker -y
sudo systemctl start docker
sudo systemctl enable docker
```
#### add your current user to the Docker group
```
sudo usermod -a -G docker ec2-user
```
##### Test Docker version
```
docker --version
docker info
```