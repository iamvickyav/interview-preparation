# docker-compose.yaml basics

docker-compose allow us to start multiple container services at a time. The configuration is written in YAML format

## Sample

Lets assume we have a EmployeeApp built using SpringBoot REST & uses MySQL for DB. Below is the sample for doing end to end containerization of the EmployeeApp application. 

### Dockerfile

```
FROM openjdk:8-jdk-alpine
COPY EmployeeApp.jar EmployeeApp.jar
CMD ["java", "-jar", "EmpApp.jar"]
```
### docker-compose.yaml

```yaml
version : '3'
services :
  webapp :
    build : .
    image : employee-app
    ports :
      - "8080:8080"
  dbapp :
    image : mysql:5.7
    restart : always
    environment :
      MYSQL_DATABASE : 'MY_DB'
      MYSQL_ROOT_PASSWORD : 'rootroot'
    expose :
      - "3306"
    ports :
      - "3306:3306"
    volumes :
      - ./sqlscript:/docker-entrypoint-initdb.d
      - ./data:/var/lib/mysql
```

### docker-compose file explained 

|   Docker-compose       |   Value                  |   Description                                                                                            |
|------------------------|--------------------------|----------------------------------------------------------------------------------------------------------|
|   version              |   3                      |   Version of Docker compose we want to use. It should be the first line in docker-compose.yaml file      |
|   services             |                          |   Configuration for each Docker container we want, is specified under services                           |
|   webapp               |                          |   User provided name for the Spring Boot web app service                                                 |
|   build                |   . (Dot)                |   Specify Dockerfile location. Use (Dot) if the Dockerfile & docker-compose.yaml are in same directory   |
|   image                |   my-img                 |   Custom Image name                                                                                      |
|   ports                |   8080:8080              |   Ports we want to expose outside of Docker container. The format is <HOST_IP>:<CONTAINER_IP>            |
|   dbapp                |                          |   User provided name for the Database container service                                                  |
|   image                |   mysql:5.7              |   Image name & its version to download from docker hub                                                   |
|   restart              |   always                 |   To restart the container every time                                                                    |
|   environment          |                          |   Environment variables we want to pass while starting the MySQL Container                               |
|   MYSQL_DATABASE       |   MY_DB                  |   Database to be created on Container startup                                                            |
|   MYSQL_ROOT_PASSWORD  |   Rootroot               |   Password for MySQL Root user account                                                                   |
|   expose               |   8080                   |   Port to be exposed for inter container communication                                                   |
|   ports                |   8080:8080              |   Ports we want to expose outside of Docker container. The format is <HOST_IP>:<CONTAINER_IP>            |
|   volumes              |   ./data:/var/lib/mysql  |   Volumes we want to mount from host to Docker container                                                 |

### Starting multiple containers with docker-compose.yaml

In order to start the application, use either of the following commands

```sh
> docker-compose up

or

> docker-compose up --build
```

<hr>

## Networking in Docker

In above docker-compose sample, we have started two containers, one for Employee Web Application & other is for MySQL Database. Typically when we want to connect Web application with MySQL, we use **connection string** like below

```
spring.datasource.url=jdbc:mysql://<b>localhost:3306</b>/MY_DB?useSSL=false&allowPublicKeyRetrieval=true
```

3306 is the default port of MySQL server. 

After we containerized the entire application, MySQL will run in its own container (read as its own operating system) whereas the Spring Boot application will be running in its own container. So localhost of SpringBoot container is not the localhost of MySQL container. Hence connecting with localhost:3306 from SpringBoot container is not gonna work

Hence we need to rely on the networking capabilities of the docker-compose to make inter-container communication possible

When we start application using `docker-compose up`, docker-compose creates a default network bridge between all the containers it start. We can refer to any container started by docker-compose using this default network bridge using the name given for the container in docker-compose.yaml file

### Fixing DB Connection between MySQL container & SpringBoot container

Replace the localhost in connection string with name given for docker container in docker-compose.yaml file can fix the inter-container communication

spring.datasource.url=jdbc:mysql://<del>localhost</del>:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true

spring.datasource.url=jdbc:mysql://**dbapp**:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true

**dbapp** is nothing but the name we given for the MySQL image in docker-compose.yaml file. Refer to line 31 above for **dpapp**

Thats all folks !!!
