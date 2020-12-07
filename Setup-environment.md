### Login to AWS Machine using SSH Client
#### Linux
```
1. Open an SSH client.
2. Locate your private key file. <keyname>.pem Run this command, if necessary, to ensure your key is not publicly viewable.
chmod 400 RaGo.pem
3. Connect to your instance using its Public IP
Example:
ssh -i "<keyname>.pem" ec2-user@<public-ip
```
for more info: Read this article about Connecting to your Linux instance : https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html
#### Windows
```
1. Open Putty Client.
2. Add your Public IP under session and save it
3. Locate your private key file.
4. Go to SSH, Then AUTH, Upload your located PPK file
5. Go to session and save again
6. Connect to your instance using its Public IP
7. Login as: ec2-user
```
for more info: Read this article about Connecting to your Linux instance : https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html
### Login to AWS Machine using EC2 Instance Connect
```
Go to the console
Select the instance
Click on Connect 
Click on Connect  once again
```

##### Install docker on Linux
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
### Exercise 1 - test docker installation
```
docker run hello-world
```
##### Check the docker image which downloaded
```
docker image ls
```
##### Check the docker image which downloaded
```
docker ps --all
```

##### Get the docker help
```
docker help
```
#### further help with a particular command
```
docker <command> --help
```
##### let's run the hello-world container
```
docker container run hello-world
```
##### let's download and run an NGINX container by running the following two commands
```
docker image pull nginx
docker container run -d --name nginx-test -p 8080:80 nginx
```
##### Stop the container
```
docker container stop nginx-test
```
##### Remove the container
```
docker container rm nginx-test
```
[Install Docker Engine in Linux](https://docs.docker.com/engine/install/)



