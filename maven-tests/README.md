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
		<groupId>com.github.garvanza</groupId>
		<artifactId>maven-tests</artifactId>
		<version>0.0.3-SNAPSHOT</version>
	</dependency>
</dependencies>
```
## Config (~/.m2/settings.xml)
```xml
<settings>
  <servers>
    <server>
      <id>github</id>
      <password>[GITHUB_TOKEN]</password>
    </server>
  </servers>
</settings>
```
## Deployment
```xml
<plugin>
	<artifactId>maven-deploy-plugin</artifactId>
	<version>2.8.1</version>
	<configuration>
		<altDeploymentRepository>internal.repo::default::file://${project.build.directory}/mvn-repo</altDeploymentRepository>
	</configuration>
</plugin>
<plugin>
	<groupId>com.github.github</groupId>
	<artifactId>site-maven-plugin</artifactId>
	<version>0.12</version>
	<configuration>
		<message>Maven artifacts for ${project.version}</message>  <!-- git commit message -->
		<noJekyll>true</noJekyll>                                  <!-- disable webpage processing -->
		<outputDirectory>${project.build.directory}/mvn-repo</outputDirectory> <!-- matches distribution management repository url above -->
		<branch>refs/heads/mvn-repo</branch>                       <!-- remote branch name -->
		<includes>
			<include>**/*</include>
		</includes>
		<repositoryName>maven-tests</repositoryName>      <!-- github repo name -->
		<repositoryOwner>garvanza</repositoryOwner>    <!-- github username -->
		<merge>true</merge>
	</configuration>
	<executions>
		<!-- run site-maven-plugin's 'site' target as part of the build's normal 
			'deploy' phase -->
		<execution>
			<goals>
				<goal>site</goal>
			</goals>
			<phase>deploy</phase>
		</execution>
	</executions>
</plugin>
```