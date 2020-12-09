### Creating an Image Including Files
Create an [index.html](index.html)
The index.html page looks like this 
```
<html>
  <body>
    <h1>Hello !</h1>
    <div>I'm hosted by a container.</div>
  </body>
</html>
```
Create a Dockerfile
```
FROM nginx:1.15
COPY index.html /usr/share/nginx/html
```
Build the image and run the container
```
docker build -t webserver .
docker run --rm -it -p 8082:80 webserver
```

