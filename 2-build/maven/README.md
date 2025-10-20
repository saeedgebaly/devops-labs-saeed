#  Lab 7: Building and Packaging Java Applications with Maven

##  Objective
Learn how to build, test, and package a Java application using **Apache Maven**.

---

##  Steps

###  Install Maven
```bash
sudo apt update
sudo apt install maven -y

# Verify installation:
mvn -v

### Clone the Source Code
git clone https://github.com/Ibrahim-Adel15/build2.git
cd build2

## Run Unit Tests
mvn test

## Build the Application
mvn package

##  Run the Application
java -jar target/hello-ivolve-1.0-SNAPSHOT.jar

## Expected output:
Hello iVolve Trainee

