#  Lab 9: Run Java Spring Boot App in a Container (Using Prebuilt JAR)

##  Objective
Run a Java Spring Boot application inside a Docker container using a **Java 17 base image** and a **prebuilt JAR file**.
---

##  Steps to Run

###  Clone the Repository
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1

## Build the Application JAR 
mvn package

## Dockerfile
FROM maven:sapmachine

WORKDIR /app

COPY target/demo-0.0.1-SNAPSHOT.jar .

EXPOSE 8080

CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]

## Explanation: 
Base Image: Maven (with Java 17)
WORKDIR: Creates a working directory /app
COPY: Copies the built JAR file into the container
EXPOSE: Opens port 8080
CMD: Runs the JAR file with java -jar

## Build the Docker Image
docker build -t app2 .

## Run the container
docker run -d --name app2-container -p 8080:8080 app2

## test
curl http://localhost:8080

## Stop and Remove the Container
docker stop app2-container
docker rm app2-container

