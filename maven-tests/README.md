# For Testing Purposes
## Maven
```xml
<repositories>
	<repository>
		<id>maven-tests-mvn-repo</id>
		<url>https://raw.github.com/garvanza/maven-tests/mvn-repo/</url>
		<snapshots>
			<enabled>true</enabled>
			<updatePolicy>daily</updatePolicy>
		</snapshots>
	</repository>
</repositories>
<dependencies>
	<dependency>
		<groupId>garvanza</groupId>
		<artifactId>maven-tests</artifactId>
		<version>0.0.3-SNAPSHOT</version>
	</dependency>
</dependencies>
```
