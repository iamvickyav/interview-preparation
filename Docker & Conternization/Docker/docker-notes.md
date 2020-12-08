# Docker notes

## Interesting Docker commands

#### To list containers (including one which is stopped)

```sh
docker container ls -a
```

#### To remove container

```sh
docker container rm <CONTAINER_ID>
```

#### To find IP address of container

```sh
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <CONTAINER_ID>
```

