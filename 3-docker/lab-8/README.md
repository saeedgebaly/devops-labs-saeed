#  Lab 8: Run Java Spring Boot App in a Container

##  Objective
Run a Java Spring Boot application inside a Docker container using a Maven base image (with Java 17).

---

##  Steps to Run

###  Clone the Repository
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1

## Dockerfile
FROM maven:sapmachine

WORKDIR /app

COPY . .

RUN mvn package

CMD ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]

EXPOSE 8080

##Explanation:
Base Image: Maven with Java 17 (sapmachine variant)
WORKDIR: Sets working directory /app
COPY: Copies the entire project
RUN mvn package: Builds the application and generates the JAR file
CMD: Runs the app using the generated JAR
EXPOSE 8080: Opens port 8080 for web access

##Build the Docker Image
docker build -t app1 .

##Run the Container
docker run -d --name app1-container -p 8080:8080 app1

##Test the Application
curl http://localhost:8080

##Stop and Remove the Container
docker stop app1-container
docker rm app1-container


