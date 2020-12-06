first dockefile
```
FROM debian:8

CMD ["echo", "Hello world"]
```

second dockerfile
```
FROM debian:8-slim

CMD ["echo", "Hello world"]
```

3rd docker file
```
FROM nginx:1.15

COPY index.html /usr/share/nginx/html
```

4th Docker file
```
FROM nginx:1.15-alpine

COPY index.html /usr/share/nginx/html
```

5th dockerfile
```
FROM debian:8

COPY . .

RUN apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -y php5
```

6th dockerfile
```
FROM debian:8

RUN apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -y php5

COPY . .
```