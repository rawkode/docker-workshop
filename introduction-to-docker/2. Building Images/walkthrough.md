# Docker Image Building

## Build Context

```shell
docker image build --tag test:one .
```

```shell
.git
```

## FROM

```Dockerfile
FROM ubuntu:18.04
```

```Dockerfile
FROM centos:6
```

```Dockerfile
FROM alpine:3.6
```

## RUN

```Dockerfile
RUN apt update && apt get install --yes vim
```

```Dockerfile
RUN yum install -y vim
```

```Dockerfile
RUN apk add --update vim
```

## COPY

```Dockerfile
# Copy a single file to a directory
COPY ./file /some/directory

# Copy whole directory
COPY . /code

# Change ownership
COPY --chown www-data:www-data . /var/www/html
```

## ADD

Same as `COPY`, with a couple of quirks:

1. Can fetch remote files
2. Extracts local archives

## EXPOSE

```Dockerfile
EXPOSE 80
```

## ENV

```Dockerfile
ENV MY_VAR="Awesome Sauce"
ENV MY_VAR_ALSO_VALID "Some Value"

# This allow multiples
ENV MY_VAR="Awesome Sauce" MY_VAR_TWO="Something Else"
```

## VOLUME

```Dockerfile
VOLUME /var/log/my-app-logs
```

## USER

```Dockerfile
USER www-data
```

## WORKDIR

```Dockerfile
WORKDIR /code

# PLEASE DON'T 😢
RUN cd /code
```


## Command Chaining

```Dockerfile
RUN apt update \
    && apt install --yes vim \
    && rm -rf /var/cache/apt
```


## ONBUILD

```Dockerfile
# More Elaborate: https://github.com/rawkode/docker-php

ONBUILD RUN if [ -f ./php-extensions.txt ]; then \
    cat ./php-extensions.txt | xargs docker-php-ext-install \
fi

ONBUILD COPY . /code
```

## Step Debugging

```shell
docker container run --rm -it some_image1 bash
apt update && apt install --yes vim
```

```shell
docker container diff container_id
docker container commit container_id some_image:2
```
