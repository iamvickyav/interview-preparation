# Spring Boot

## What is Spring Boot ?

According to Spring Team

> Spring Boot helps you to create stand-alone, production-grade Spring-based applications that you can run. We take an opinionated view of the Spring platform and third-party libraries, so that you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration

## Getting Started

To get started with Spring boot, install Java & Maven/Gradle. This guide will use Maven going forward

Lets say, we want to create an application which exposes REST endpoints. 

All we need to do is create a maven project in IDE (say IntelliJ Idea/Eclipse) & add few dependencies in pom.xml file

### pom.xml from scratch

**pom.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.6</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
</project>
```

Since we added spring-boot-starter-web under dependency, Spring Boot understands we are trying to create a web application & it will configure lot of basic stuff for us 

ok what basic stuff ? 

Any web application needs an application server to run right ? So spring-boot-starter-web will add **Tomcat** JAR in our classpath by default. 

spring-boot-starter-web dependency will also add JSON processing library called Jackson to our classpath. After all, what good a web application is, if its not using JSON in 2021 ? So Spring Boot will add the Jackson library to our classpath. 

But why Jackson library ? why not GSON (JSON processing library from Google) to process JSON ? 

This is where the opinions of Spring team comes into play. They believe Jackson library is the best out there to work with JSON. Same goes for Tomcat. 

Thats why Spring Boot is referred as **OPINIONATED FRAMEWORK**

Ok but I don't like Tomcat. I prefer Jetty server. Is there a way to tell Spring Boot to use Jetty instead of Tomcat ? Of course there are ways to configure it. Here is where the idea of Convention over configuration comes into play. Spring team came with defaults but we developers can still override them & configure

Here is how to use Jetty server instead of Tomcat in Spring Boot

**pom.xml**

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
	    <exclusion>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
		</exclusion>
	</exclusions>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

If you are familiar with Maven already, you would have noticed, we didn't mention <version> tag under any dependency. Then which version spring-boot-starter-web will get downloaded ?

Thats where the <parent> comes into play

### Understanding spring-boot-starter-parent

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.5.6</version>
</parent>
```

According to Spring documentation, 

> The spring-boot-starter-parent is a special starter that provides useful Maven defaults. It also provides a dependency-management section so that you can omit version tags for “blessed” dependencies.

