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

Under services, we can specify any number of services. From the above same docker-compose.yaml file, lets take services one by one to understand them

### Service 1

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
```

### Service 2

```
# solr is the name I chose for the service. You can choose any name
  solr:
  
    # If you notice, I haven't specified anything called build. Because I am not gonna build any custom image. Instead I am gonna pull solr image from docker hub. Hence image: solr:7.6
    image: solr:7.6
    
    # Expose the service via port 8983
    ports:
      - "8983:8983"
      
    # Mount volume from local system to Docker directory to persist 
    volumes:
      - ./solr_cores/IndianTowns:/opt/solr/server/solr/IndianTowns
 ```

