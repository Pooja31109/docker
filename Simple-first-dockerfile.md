### Creating a simple image
```
touch Dockerfile

# Open your Dockerfile with your preferable editor
vim Dockerfile

# Write First line as 
FROM debian:8

# Second line as 

CMD ["echo", "Hello Docker Class!!"]

# build the docker image using dockerfile
docker build -t hello-class .

# run the container using hello-class image
docker run --rm hello
```
The final dockerfile looks like below
```
FROM debian:8
CMD ["echo", "Hello Docker Class!!"]
```