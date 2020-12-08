# Docker Commands

## Interesting Docker commands

### Container commands

#### To list containers (including one which is stopped)

```sh
docker container ls -a
```

#### To list only id of containers (including one which is stopped)

```sh
docker container ls -aq
```

#### To remove a container

```sh
docker container rm <CONTAINER_ID>
```

#### To remove all stop containers

```sh
docker container rm $(docker container ls –aq)
```

#### To mount volume in container to outside world

```sh
docker run -p 8080:8080 -v /usr/local/tomcat/logs:/Users/jarvis/Downloads/logs d991231dccdf
```

#### To find IP address of container

```sh
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <CONTAINER_ID>
```

