# Docker Session 2 Notes

Consider we have a Simple Spring Boot application which exposes REST endpoints to fetch Employee records from MySQL Database.

In Below, we explained step by step on how we can Dockerize the entire application

<hr/>

### Stage 1 : Both SpringBoot App & DB Running in local (host system)

<hr/>

**DB Connection String**

`jdbc:mysql://localhost:3306/MY_DB`

**Dockerfile** 

Not applicable (N/A)

**Docker-compose.yaml** 

N/A

<hr/>

### Stage 2 : SpringBoot App containerized using Dockerfile & DB Running in local (host system)

<hr/>

**DB Connection String**

`jdbc:mysql://host.docker.internal:3306/MY_DB`

**Dockerfile**
```
FROM openjdk:8-jdk-alpine
COPY EmpApp.jar EmpApp.jar
CMD ["java", "-jar", "EmpApp.jar"]
```

**Docker-compose.yaml**

N/A

<hr/>

### Stage 3 :  SpringBoot App containerized using docker-compose.yaml & DB Running in local (host system)

<hr/>

**DB Connection String**

`jdbc:mysql://host.docker.internal:3306/MY_DB`

**Dockerfile**

```
FROM openjdk:8-jdk-alpine
COPY EmpApp.jar EmpApp.jar
CMD ["java", "-jar", "EmpApp.jar"]
```

**Docker-compose.yaml**

```
version : '3'
services:
  web:
    image : emp-compose-img
    build : .
    ports :
      - "8080:8080"
```
<hr/>

### Stage 4 :  Both SpringBoot App & MySQL DB containerized using docker-compose.yaml

<hr/>

**DB Connection String**

`jdbc:mysql://db:3306/MY_DB`

**Dockerfile**

```
FROM openjdk:8-jdk-alpine
COPY EmpApp.jar EmpApp.jar
CMD ["java", "-jar", "EmpApp.jar"]
```

**Docker-compose.yaml**

```
version : '3'
services:
  web:
    image : emp-compose-img
    build : .
    ports :
      - "8080:8080"
  db:
    image : mysql:5.7
    restart : always
    environment:
      MYSQL_DATABASE: 'MY_DB'
      MYSQL_ROOT_PASSWORD: 'rootroot'
    expose :
      - "3306"
    volumes:
      - ./scripts:/docker-entrypoint-initdb.d
      - ./data:/var/lib/mysql
```

