# Docker Multi-Stage Image Building

```Dockerfile
FROM ubuntu:18.04 AS base

COPY --from=base ? ?

COPY --from=0 ? ?
```

```shell
docker image build -t tag --target base .
```

## DIND

```shell
docker container run -v /var/run/docker.sock:/var/run/docker.sock docker:dind
```
