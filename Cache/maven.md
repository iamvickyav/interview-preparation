Maven

It is a a project management tool provides superset of features found in a build tool like Ant

Maven prefers Convention Over Configuration approach. Hence it make few default assumptions like below (which can be customized if needed)

Source code is assumed to be in /src/main/java
Resource is assumed to be in /src/main/resources

pom.xml

Maven relies on Project Object Model (pom.xml) file where we specify the Maven configuration

All Maven project pom files extend the Super POM, which defines set of defaults

```
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.iamvickyav</groupId>
	<artifactId>first-project</artifactId>
	<version>1.0</version>
</project>
```

Dependencies

3rd party library dependencies are defined using <dependency> tag

Scope

* compile
* provided
* runtime
* test




