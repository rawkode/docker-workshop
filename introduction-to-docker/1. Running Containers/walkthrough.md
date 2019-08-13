# Docker Essentials

## Docker Version

We're ideally looking for >= 17.06. 1.13 should be OK


```shell
docker version
```

## Hello, world!

```shell
docker container run hello-world
```

## Ubuntu

😮

```shell
docker container run -it ubuntu:18.04
```

😧

```shell
figlet Hello, Docker Workshop
```

😄

```
apt update && apt install --yes figlet
figlet Hello, Docker Workshop
```

⚠️

```shell
docker container run hello-world
figlet Hello, Docker Workshop
```


## Web Servers

```shell
docker container run -P httpd
docker container port ID
```

```shell
docker container run -p 8080:80 httpd
```

## Volumes

```shell
docker container run --name data --volume=/data -it ubuntu:18.04 bash
docker container run --volumes-from=data -it ubuntu:18.04 bash
```

## Named Volumes

```shell
docker volume create my_data_volume
docker container run --volume=my_data_volume:/data -it ubuntu:18.04 bash
docker container ls -aq | xargs docker container rm -f
```

## Bind Mounts

```shell
docker container run --volume=/home/rawkode:/home/rawkode -it ubuntu:18.04 bash
```

## Links

```shell
docker container run --detach --name=mongodb -it mongo:3.6 bash
docker container run --link=mongodb:mongodb -it ubuntu:18.04 bash
```
