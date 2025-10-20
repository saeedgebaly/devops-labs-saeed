#  Lab 6: Building and Packaging Java Applications with Gradle

##  Objective
Learn how to build, test, and package a Java application using **Gradle**.

---

##  Steps

###  Install Gradle
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install gradle

## Verify installation:
gradle -v
java -version

### Clone the Source Code
git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1

### Run Unit Tests
gradle test

### Build the Application
gradle build

### Run the Application
java -jar build/libs/ivolve-app.jar

(Hello iVolve Trainee)
