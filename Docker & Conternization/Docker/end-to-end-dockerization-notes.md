# Docker Session 2 Notes

In our sample application, we had a Spring Boot application & MySQL Database. Initially we started with having both Spring Boot Application & MySQL Database in our local system. Then we Dockerized them one by one. Based on Dockerization, the connection string to DB from Spring Boot app was changed accordingly. 

In Below, we captured step by step on how we Dockerized an entire application from scratch 

<hr/>

### Scenario 1 : Both SpringBoot App & DB Running in local (host system)

<hr/>

**DB Connection String**

`jdbc:mysql://localhost:3306/MY_DB`

**Dockerfile** 

Not applicable (N/A)

**Docker-compose.yaml** 

N/A

<hr/>

### Scenario 2 : SpringBoot App containerized using Dockerfile & DB Running in local (host system)

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

### Scenario 3 :  SpringBoot App containerized using docker-compose.yaml & DB Running in local (host system)

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

### Scenario 4 :  Both SpringBoot App & MySQL DB containerized using docker-compose.yaml

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

