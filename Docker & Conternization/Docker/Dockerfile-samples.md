# Dockerfile Samples

## Alpine Linux Distribution + Java

```
FROM alpine:3.11
RUN apk add openjdk11
CMD ["/usr/bin/java", "-version"]
```

## Alpine Linux Distribution + Tomcat
```
FROM tomcat:8.5.21-jre8-alpine
COPY target/Sample.war /usr/local/tomcat/webapps
ENTRYPOINT ["catalina.sh", "start"]
```
