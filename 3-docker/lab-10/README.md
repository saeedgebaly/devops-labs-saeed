#  Lab 10: Multi-Stage Build for a Spring Boot App

##  Objective
In this lab, we learned how to use **Docker multi-stage builds** to create a lightweight production image for a Spring Boot (Java) application.

---

##  Steps

###  Clone the Application Repository
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1

## Create a Dockerfile with Multi-Stage Build

# Stage 1: Build stage using Maven
FROM maven:sapmachine AS build
WORKDIR /app
COPY . .
RUN mvn package -DskipTests

# Stage 2: Run stage using Java
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]

## Build the Image
docker build -t app3 .

## Check the Image Size
docker images

## Run the Container
docker run -d -p 8080:8080 --name app3-container app3

## Test the Application
curl http://localhost:8080

## Stop and Remove the Container
docker stop app3-container
docker rm app3-container

