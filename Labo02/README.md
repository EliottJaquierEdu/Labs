# Labo02 - Run a Spring App Locally

## Pedagogical intent
In this lab, we'll be taking the application we're going to evolve into our own hands, to discover the Spring architecture.

---

## Task 01 - Run the app

### Use Maven to package the solution

* [Maven Doc](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html#build-the-project)

```bash
mvn package
```

* What operation does maven perform ?

```
//Fetch dependencies, copy-resources, compile, tests, report, build jar, repackage
```

* What java dependencies are needed to make this work?

```
//In summary : Spring Boot, Javax cache, Webjars, H2Database, XML Bind, Junit, MySQL (Connector), Postgress, Caffeine 
```

* Where do we find the pre-compiled application after that?

```
//Under target (target\spring-petclinic-3.2.0-SNAPSHOT.jar)
```

* Delete the folder containing the pre-compiled application, try again to observe the process.

* Is it a build ready for prod ?

```
//No, it is a snapshot. It's not meant to go in a production env.
```

### Use Java to launch the application

* [The java command](https://docs.oracle.com/en/java/javase/14/docs/specs/man/java.html)

```bash
java -jar .\target\spring-petclinic-3.2.0-SNAPSHOT.jar
```

* Try to access to the app via your browser

```
//localhost:8080
```

* You should get this page

![Home Page](img/webappSample.JPG)

* Stop the app

## Use the Spring Boot Maven plugin to launch the application

* [Maven plug in to run the app](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#run)

```bash
mvn spring-boot:run
```

---

## Task 02 - Explore the app

### Kind of app

* How can we access a home page via our browser?

```
When starting the java application, spring boot start a serverlet. 
The implementation used on this app is an embeded Apache Tomcat web server.
//TODO : Find where tomcat interact with the spring router.
Next, a rooter determine the controller and method to go by going through @GetMapping anotation.
The welcome controller simply return the 'welcome' view, a HTML template.
```

* Go to http://localhost:8080/owners/find and add an owner

* Using the search function, can you find it?

* Relaunch the application and try again. How is data persistence ensured?

```
The data is destroyed. Is it beacause it's a database in RAM or file is destroyed or schema is re-run? I'm not sure.
```

* How many logic layers are implemented on this application?

```
4 :
Presentation Layer
Business Layer – Business Logic, Validation & Authorization
Persistence Layer – Storage Logic
Database Layer – Actual Database
```

---
## Task 03 - Docker - First Analysis

* At this stage of the analysis, can you imagine a little better what kind of needs Docker could help us with?

```
We could have a docker for building the app (full JDK suite / all tools) and then publish a production, minimal docker with only the jar / war and a JRE.
We can split the project to use microservices by business (owner, vet, etc...) or layer (one container for database, one for business logic and one for web application)
```

* Try to list the tasks to be carried out to obtain two thirds, one hosting the application part locally and the second third using Docker for the database engine.

```
- Ask questions (like will the database know business entities / have spring ? or simply a docker with a database only and the main application will query the remote docker with SQL?)
- Research docker / find a clean database type image
- Split application 
- (Create a clean container builder) not usefull for now. No need for Ci/CD pipeline either.
- Configure app to use a remote database
- Find a place to publish the database image
- (Deploy the container to AWS, research, awscli, configure, etc...)
```
