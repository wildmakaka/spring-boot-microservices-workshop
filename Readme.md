# [Java Brains] Spring Boot Microservices [ENG, 2019]

<br/>

**YouTube:**  
https://www.youtube.com/c/JavaBrainsChannel/playlists?view=50&sort=dd&shelf_id=4


<br/>

**original src:**  
https://github.com/koushikkothagal/spring-boot-microservices-workshop

<br/>

```
$ cd apps
```

<br/>


```
$ curl https://start.spring.io/starter.zip \
  -d language=java \
  -d javaVersion=11 \
  -d platformVersion=2.6.1 \
  -d dependencies=web,webflux,cloud-eureka \
  -d packaging=jar \
  -d jvmVersion=11 \
  -d groupId=org.javadev \
  -d artifactId=movie-catalog-service \
  -d name=movie-catalog-service \
  -d description=Spring%20Boot%20Microservices \
  -d packageName=org.javadev.movie-catalog-service \
  -o movie-catalog-service.zip


$ curl https://start.spring.io/starter.zip \
  -d language=java \
  -d javaVersion=11 \
  -d platformVersion=2.6.1 \
  -d dependencies=web,cloud-eureka \
  -d packaging=jar \
  -d jvmVersion=11 \
  -d groupId=org.javadev \
  -d artifactId=ratings-data-service \
  -d name=ratings-data-service \
  -d description=Spring%20Boot%20Microservices \
  -d packageName=org.javadev.ratings-data-service \
  -o ratings-data-service.zip
 

$ curl https://start.spring.io/starter.zip \
  -d language=java \
  -d javaVersion=11 \
  -d platformVersion=2.6.1 \
  -d dependencies=web,cloud-eureka \
  -d packaging=jar \
  -d jvmVersion=11 \
  -d groupId=org.javadev \
  -d artifactId=movie-info-service \
  -d name=movie-info-service \
  -d description=Spring%20Boot%20Microservices \
  -d packageName=org.javadev.movie-info-service \
  -o movie-info-service.zip

$ curl https://start.spring.io/starter.zip \
  -d language=java \
  -d javaVersion=11 \
  -d platformVersion=2.6.1 \
  -d dependencies=cloud-eureka-server \
  -d packaging=jar \
  -d jvmVersion=11 \
  -d groupId=org.javadev \
  -d artifactId=discovery-server \
  -d name=discovery-server \
  -d description=Spring%20Boot%20Microservices \
  -d packageName=org.javadev.discovery-server \
  -o discovery-server.zip
```

<br/>

```
$ unzip movie-catalog-service.zip -d ./movie-catalog-service
$ unzip ratings-data-service.zip  -d ./ratings-data-service
$ unzip movie-info-service.zip  -d ./movie-info-service
$ unzip discovery-server.zip  -d ./discovery-server
```

<br/>

```
$ rm movie-catalog-service.zip
$ rm ratings-data-service.zip
$ rm movie-info-service.zip
$ rm discovery-server.zip
```

<br/>

```
$ ./mvnw spring-boot:run
```

<br/>

http://localhost:8081/catalog/foo

<br/>


**movie-catalog-service/pom.xml**

<br/>

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```

<br/>

### 19 Starting a Eureka server


**DiscoveryServerApplication.java**

<br/>

```
***
@EnableEurekaServer
***
```

<br/>

```
$ vi src/main/resources/application.properties 
```

<br/>

```
server.port=8761
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

<br/>

http://localhost:8761/

<br/>

OK!


<!--

<br/>


**discovery-server/pom.xml**

<br/>

???

<br/>

```xml
  <dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.0</version>
  </dependency>
  <dependency>
    <groupId>com.sun.xml.bind</groupId>
    <artifactId>jaxb-impl</artifactId>
    <version>2.3.0</version>
  </dependency>
  <dependency>
    <groupId>org.glassfish.jaxb</groupId>
    <artifactId>jaxb-runtime</artifactId>
    <version>2.3.0</version>
  </dependency>
  <dependency>
    <groupId>javax.activation</groupId>
    <artifactId>activation</artifactId>
    <version>1.1.1</version>
  </dependency>
```

-->


<br/>


**movie-info-service/pom.xml**

<br/>

```xml
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>
```


<br/>


```
<spring-cloud.version>Greenwich.RELEASE</spring-cloud.version>
```

<br/>

```xml
	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
```


<br/>

```xml
	<repositories>
		<repository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
		</repository>
	</repositories>
```

