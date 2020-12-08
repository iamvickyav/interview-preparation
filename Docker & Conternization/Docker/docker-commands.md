# Docker Commands

### General Commands

#### Open bash inside Container

```sh
docker exec -it d541afb504bd bash
```

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
docker run -p 8080:8080 -v /usr/local/tomcat/logs:/Users/jarvis/Downloads/logs <IMAGE_ID>
```

#### To find IP address of container

```sh
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <CONTAINER_ID>
```

#### logs

```sh
docker logs <CONTAINER_ID>
```

