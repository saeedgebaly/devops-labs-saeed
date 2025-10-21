# Lab 11: Managing Docker Environment Variables Across Build and Runtime

##  Objective
This lab demonstrates **three different ways** to manage environment variables in Docker for a Python Flask application:
1. Inside the **Dockerfile**
2. Using **environment variables in the run command**
3. Using an **environment file (.env)**

---

##  Step 1: Clone the Application Code
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3

## Step 2: Create Dockerfiles
 #Dockerfile
Used for methods 1 and 2

dockerfile
Copy code
FROM python:3.9

WORKDIR /app
COPY . .

RUN pip install flask

EXPOSE 8080

CMD ["python", "app.py"]
  #Dockerfile2
Used for method 3 (production)

dockerfile
Copy code
FROM python:3.9

WORKDIR /app
COPY . .

RUN pip install flask

# Environment variables inside Dockerfile
ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python", "app.py"]
## Step 3: Sample app.py
Make sure your Flask app prints environment variables:

python
Copy code
from flask import Flask
import os

app = Flask(__name__)

@app.route('/')
def home():
    return f"App Mode: {os.getenv('APP_MODE')} | Region: {os.getenv('APP_REGION')}"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
## Step 4: Create Environment File
Create a file named env:

ini
Copy code
APP_MODE=staging
APP_REGION=us-west
## Step 5: Build and Run in 3 Different Ways
# Method 1 — Command Line Variables (Development)
bash
Copy code
docker build -t app-dev -f Dockerfile .
docker run -d -p 8081:8080 \
-e APP_MODE=development \
-e APP_REGION=us-east \
app-dev
Access:

bash
Copy code
curl localhost:8081
Expected Output:

yaml
Copy code
App Mode: development | Region: us-east
# Method 2 — Env File Variables (Staging)
bash
Copy code
docker run -d -p 8082:8080 --env-file env app-dev
Access:

bash
Copy code
curl localhost:8082
Expected Output:

yaml
Copy code
App Mode: staging | Region: us-west
# Method 3 — Dockerfile Variables (Production)
bash
Copy code
docker build -t app-prod -f Dockerfile2 .
docker run -d -p 8083:8080 app-prod
Access:

bash
Copy code
curl localhost:8083
Expected Output:

yaml
Copy code
App Mode: production | Region: canada-west