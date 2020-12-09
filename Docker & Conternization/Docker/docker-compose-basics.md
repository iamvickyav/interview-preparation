# docker-compose.yaml basics

## Introduction

When we want to run Multicontainer Docker application, we have to go for docker-compose. 

docker-compose can able to start multiple container services at a time. The configuration is written in YAML format in a file called docker-compose.yaml

Here is a sample docker-compose.yaml file

```
version : '3'
services:
  web:
    build: .
    image: web-app
    ports:
      - "8080:8080"
  solr:
    image: solr:7.6
    ports:
      - "8983:8983"
    volumes:
      - ./solr_cores/IndianTowns:/opt/solr/server/solr/IndianTowns
 ```

version refers to the version of docker-compose we are gonna use

## Services in docker-compose

We can specify any number of service under services label. I took the above docker-compose.yaml content & added comments for better understanding

```
# web is the name I chose for the service. You can choose any name
web:
    # build customer Docker image from Dockerfile mentioned in current directory (since I specified .(dot), it will look for Dockerfile in current directory)
    build: .
    
    # Name the image as web-app
    image: web-app
    
    # Expose the service via port 8080
    ports:
      - "8080:8080"
      
   # solr is the name I chose for the service. You can choose any name
  solr:
  
    # If you notice, I haven't specified anything called build. Because I am not gonna build any custom image. Instead I am   gonna pull solr image from docker hub. Hence image: solr:7.6
    image: solr:7.6
    
    # Expose the service via port 8983
    ports:
      - "8983:8983"
      
    # Mount volume from local system to Docker directory to persist 
    volumes:
      - ./solr_cores/IndianTowns:/opt/solr/server/solr/IndianTowns
 ```
 
## Networking in docker-compose.yaml
 
Services metioned in docker-compose can interact with one another using default network provided by Docker. For interaction, they need to use service name specified in docker-compose.yaml file

Confused ??? Let me explain with an example

Lets say we have a Demo web application developed using SpringBoot which uses MySQL as database. We install MySQL in local & we deploy WAR file in local Tomcat. Typically the connection string to DB be like this

```
spring.datasource.url=jdbc:mysql://localhost:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true
```

Now we want to containerize this entire application by moving Tomcat & MySQL to Docker. so we will typically create a Dockerfile & docker-compose.yaml like below

**Dockerfile**
```
FROM tomcat:latest
ADD target/demo.war /usr/local/tomcat/webapps/
CMD ["catalina.sh", "run"]
```

**docker-compose.yaml**
```
version : '3'
services:
  web:
    build: .
    image: web-app
    ports:
      - "8080:8080"
   mysql-db:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    environment:
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "3306:3306"
```

To start the application, all you have to do it below

```
> mvn clean package
> docker-compose up
```

But the application will eventually fail because of the incorrect connection string we failed to fix

```
spring.datasource.url=jdbc:mysql://localhost:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true
```

Since the Tomcat is running inside Docker, we can't say localhost:3306 to refer to MySQL db. MySQL is running inside another docker container.

hence we have to change the query string with name (mysql-db) we specified in docker-compose.yaml

```
spring.datasource.url=jdbc:mysql://mysql-db:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true
```

Thats all folks !!!


```
version : '3'
services :
  web :
    build : .
    image: web-app
    ports :
      - "8080:8080"
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: 'MY_DB'
      MYSQL_ROOT_PASSWORD: 'rootroot'
    ports:
      - '3306:3306'
    expose:
      - '3306'
    volumes:
      - /Users/jarvis/Downloads/mysql-sample/src/main/resources:/docker-entrypoint-initdb.d
      - ./data:/var/lib/mysql
```
