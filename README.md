# Cagri Altug
# knapsack-optimizer

[![CircleCI](https://circleci.com/gh/altugcagri/knapsack-optimizer/tree/master.svg?style=svg&circle-token=d22fffb09eefdc77fbc1ca5f143253613da04e21)](https://circleci.com/gh/altugcagri/knapsack-optimizer/tree/master)

## Problem

In the Knapsack problem, one specifies the weights and values of a collection of items and the capacity of a knapsack, and is looking for a way to pack some of the items, up to the capacity constraint, to maximise the total value of the knapsack's content.    
[Wikipedia article](https://en.wikipedia.org/wiki/Knapsack_problem).

## The task
You are asked to develop a *web service* that will allow a user to:

* specify the parameters of a knapsack problem (weights and values of items, capacity);
* execute the optimiser;
* retrieve the solution.

## Installation

In order to install and run the project [Java](https://www.java.com) Jdk v8+ and [Gradle](https://gradle.org/) must be installed.

Set JAVA_HOME like "C:\Program Files\Java\jdk1.8.0_12", "bin" folder is not required. Otherwise gradle tasks can fail.

In order to run the project on docker environment [Docker](https://docs.docker.com/) must be installed.

After installation  of Java, Gradle and Docker, you can clone the project from the [repository](https://github.com/altugcagri/knapsack-optimizer.git) into your workspace.

## Build

After cloning the project go to workspace and run the gradle command:

```sh
$ .\gradlew build
```

in order to run tests run the gradle command:

```sh
$ .\gradlew test
```

## Run Without Docker Containerization

After building the project running the project requires the steps below;

Since project requires eureka-server and zuul-server, first these two services should run respectively.

eureka-server:

```sh
$ java -jar eureka-server\build\libs\eureka-server-0.0.1-SNAPSHOT.jar
```

zuul-server:

```sh
$ java -jar zuul-server\build\libs\zuul-server-0.0.1-SNAPSHOT.jar
```

knapsack-optimizer-service:

```sh
$ java -jar build/libs/knapsack.optimizer-0.0.1-SNAPSHOT.jar
```

## Run With Docker Containerization

After building the project, Simply run the commands according to your scalability choice;

In the directory where docker-compose.yml exists

one instance from knapsack-optimizer-service:

```sh
$ docker-compose up
```

n instance from knapsack-optimizer-service where n is an integer;

```sh
$ docker-compose up --scale knapsack-optimizer-service=n
```

## Monitoring 

After running the project, you can simply monitor instances on the eureka server console by navigating the url in your preferred browser.

```
http://localhost:8761/
```

![eureaka-server](docs/eureaka-server.png "eureaka-server")

Status check can be done by the url in your preferred browser

```
http://localhost:8762/actuator/health
```

or by using curl

```sh
$ curl http://localhost:8762/actuator/health
```
Excepted result

```
{"status":"UP"}
```

Information check about the knapsack optimizer service can done by the url in your preferred browser

```
http://localhost:8762/actuator/info
```

or by using curl

```sh
$ curl http://localhost:8762/actuator/info
```
Excepted result

```
{
   "app":{
      "name":"Knapsack Optimiser Service",
      "descrition":"Spring boot application which serves solution to knapsack problem. This challenge application is designed for the Maersk Digital ",
      "version":"0.0.1-SNAPSHOT"
   }
}
```

## REST API

After running the project, detailed documentation can be found from the url below

```
$ http://localhost:8762/swagger-ui.html#/knapsack-rest-api
```

or by using curl, you can get swagger json 

```sh
$ curl http://localhost:8762/v2/api-docs
```

## Architecture

### Package Structure

High level package structure of the project is represented below;

    .
    ├── .cicleCI                      # CircleCI integraion
    │   └── config.yml                # Configuration for ci/cd pipeline of CircleCI
    ├── docs                          # Documentation files (alternatively `doc`)
    │   ├── eureaka-server.png        # Eureka console screenshot
    │   ├── knapsack-optimizer.png    # Class diagram of knapsack-optimizer
    │   ├── knapsack-optimizer.uml    # Class diagram of knapsack-optimizer in uml format
    │   └── system-architecture.png   # System architectur overview
    ├── eureaka-server                # Spring boot application for discoversy service
    ├── gradle/wraper                 # Build tools
    ├── src                           # Source files of knapsack-optimizer-service
    ├── zuul-server                   # Spring boot application for load balancing
    ├── Dockerfile                    # Containerization of knapsack-optimizer-service
    ├── build.gradle                  # Build scrips of knapsack-optimizer-service
    ├── docker-compose.yml            # Orchestration of containers
    ├── gradlew                       # Gradle commands
    ├── gradlew.bat                   # Gradle commands file
    └── settings.gradle               # Project settings

### Class Diagram

Class diagram of the knapsack-optimizer-service is represented below;

![eureaka-server](docs/kapsack-optimizer.png "eureaka-server")

### System Overview

System overview of the project is represented below;

![System Overview](docs/system-architecture.png "System Overview")


### Dependencies

####knapsack-optimizer-service

* [Spring Boot](https://spring.io/projects/spring-boot) - The Spring Boot framework is used as base.
* [Spring Cloud](https://spring.io/projects/spring-cloud) - The Spring Cloud framework is used in order to eureka services.
* [Swagger](https://swagger.io/) - Swagger dependency is used for documentation of the API.
* [Lombok](https://projectlombok.org/) - Lombok dependency is used.
* [JUnit](http://junit.org) - JUnit is used for unit testing.
* [Mockito](http://site.mockito.org) - Mockito is used for mocking the objects in unit tests.
* [Gradle](https://gradle.org/) - Gradle is used for dependency management and build.
* [Docker](https://docs.docker.com/) - Docker is used for containers.
* [Java](https://www.java.com) - Java language is used as programming language.
* [Intellij IDEA](https://www.jetbrains.com/idea/) - An open source IDE for Java projects.

####eureka-server

* [Spring Boot](https://spring.io/projects/spring-boot) - The Spring Boot framework is used as base.
* [Spring Cloud](https://spring.io/projects/spring-cloud) - The Spring Cloud framework is used in order to eureka services.
* [Gradle](https://gradle.org/) - Gradle is used for dependency management and build.
* [Docker](https://docs.docker.com/) - Docker is used for containers.
* [Java](https://www.java.com) - Java language is used as programming language.
* [Intellij IDEA](https://www.jetbrains.com/idea/) - An open source IDE for Java projects.

####zuul-server

* [Spring Boot](https://spring.io/projects/spring-boot) - The Spring Boot framework is used as base.
* [Spring Cloud](https://spring.io/projects/spring-cloud) - The Spring Cloud framework is used in order to eureka and zuul services.
* [Gradle](https://gradle.org/) - Gradle is used for dependency management and build.
* [Docker](https://docs.docker.com/) - Docker is used for containers.
* [Java](https://www.java.com)- Java language is used as programming language.
* [Intellij IDEA](https://www.jetbrains.com/idea/) - An open source IDE for Java projects.

## Improvements

For further improvement, 

* Security implementations can be added through WebConfig.java
* Different algorithms can be implemented to the system like [Google Optimization Tools](https://developers.google.com/optimization/bin/knapsack)
* In the pipeline, only test task exists to check the tests results. Building the project and delivering to some clouds environments like [AWS](https://aws.amazon.com/) or [AZURE](https://azure.microsoft.com/en-us/) can be implemented.

## References
[The Knapsack Problem](https://rerun.me/2014/05/27/the-knapsack-problem/)

