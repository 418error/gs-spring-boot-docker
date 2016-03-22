# gs-spring-boot-docker

#### Built using...
* A Mac
* Atom
* Java JDK 1.8
* Gradle 2.10

#### The steps...

1. Create a project folder

  ```
  mkdir gs-spring-boot-docker
  cd gs-spring-boot-docker
  ```
2. Create a Gradle build script
  ```
  touch build.gradle
  atom build.gradle
  ```
  Copy the contents from this [Initial Gradle build script](  https://github.com/spring-guides/gs-spring-boot-docker/blob/master/initial/build.gradle) to the build.gradle file

3. Create the project directory structure
  ```
  mkdir -p src/main/java/hello
  ```

4. Create a domain class
  ```
  touch src/main/java/hello/Application.java
  atom src/main/java/hello/Application.java
  ```
  Add the following

  ```java
  package hello;

  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.boot.bind.RelaxedPropertyResolver;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;

  @SpringBootApplication
  @RestController
  public class Application {

  	@RequestMapping("/")
  	public String home() {
  		return "Hello Docker World";
  	}


  	public static void main(String[] args) {
  		SpringApplication.run(Application.class, args);
  	}

  }
  ```
5. Run it
  * The one liner
  ```
  gradle bootRun
  ```
  * Build and run
  ```
  gradle Build && java -jar build/libs/gs-spring-boot-docker-0.1.0.jar
  ```

  Go to <http://localhost:8080/> to see your "Hello Docker World" message.

6. Containerize It
  ```
  touch src/main/docker/Dockerfile
  atom src/main/docker/Dockerfile
  ```
  Add the following
  ```
  FROM frolvlad/alpine-oraclejdk8:slim
  VOLUME /tmp
  ADD gs-spring-boot-docker-0.1.0.jar app.jar
  RUN bash -c 'touch /app.jar'
  ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
  ```
  
