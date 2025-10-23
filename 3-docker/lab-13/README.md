Lab 13: Custom Docker Network for Microservices

Objective



In this lab, we will create a custom Docker network and connect multiple microservices (frontend and backend) to it to verify inter-container communication.



Steps

1\. Clone the Repository

git clone https://github.com/Ibrahim-Adel15/Docker5.git

cd Docker5



2\. Create Dockerfile for Frontend



Create a file named Dockerfile.frontend inside the frontend directory:



\# Dockerfile.frontend

FROM python:3.9



WORKDIR /app



COPY . .



\# Install ping utility and Python dependencies

RUN apt-get update \&\& apt-get install -y iputils-ping \&\& rm -rf /var/lib/apt/lists/\*

RUN pip install -r requirements.txt



EXPOSE 5000



CMD \["python", "app.py"]





Build the image:



docker build -t frontend-img -f Dockerfile.frontend .



3\. Create Dockerfile for Backend



Create a file named Dockerfile.backend inside the backend directory:



\# Dockerfile.backend

FROM python:3.9



WORKDIR /app



COPY . .



\# Install ping utility and Flask

RUN apt-get update \&\& apt-get install -y iputils-ping \&\& rm -rf /var/lib/apt/lists/\*

RUN pip install flask



EXPOSE 5000



CMD \["python", "app.py"]





Build the image:



docker build -t backend-img -f Dockerfile.backend .



4\. Create a Custom Docker Network

docker network create ivolve-network





Verify the network:



docker network ls



5\. Run Containers on the Network

Run the Backend Container:

docker run -d --name backend --network ivolve-network backend-img



Run the Frontend Container (frontend1) on the Same Network:

docker run -d --name frontend1 --network ivolve-network frontend-img



Run Another Frontend Container (frontend2) on the Default Bridge Network:

docker run -d --name frontend2 frontend-img



\## Verify Communication Between Containers

\## Test connection between frontend1 and backend (same network):

docker exec -it frontend1 ping backend





You should see successful ping replies.



\## Test connection between frontend2 and backend (different networks):

docker exec -it frontend2 ping backend





You should get an error, meaning they cannot communicate.



7\. Clean Up



Stop and remove containers:



docker rm -f frontend1 frontend2 backend





Remove the custom network:



docker network rm ivolve-network

