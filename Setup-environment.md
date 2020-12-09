### Login to AWS Machine using SSH Client
#### Linux
```
1. Open an SSH client.
2. Locate your private key file. <keyname>.pem 
Run below command, if necessary, to ensure your key is not publicly viewable.
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

[Install Docker Engine in Linux](https://docs.docker.com/engine/install/)



