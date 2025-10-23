

\##  Objective

Deploy a Node.js application that connects to a MySQL database using \*\*Docker Compose\*\*.  

The application requires a database named \*\*`ivolve`\*\* to start successfully.



---



\##  Steps



\###  Clone the Source Code

```bash

git clone https://github.com/Ibrahim-Adel15/kubernets-app.git

cd kubernets-app

2-  Create the Docker Compose File

Create a file named docker-compose.yml:



yaml

Copy code

version: '3.9'



services:

&nbsp; app:

&nbsp;   build: .

&nbsp;   container\_name: node-app

&nbsp;   ports:

&nbsp;     - "3000:3000"

&nbsp;   depends\_on:

&nbsp;     - db

&nbsp;   environment:

&nbsp;     DB\_HOST: db

&nbsp;     DB\_USER: app

&nbsp;     DB\_PASSWORD: 12345

&nbsp;     DB\_PORT: 3306

&nbsp;   volumes:

&nbsp;     - ./logs:/app/logs



&nbsp; db:

&nbsp;   image: mysql:8

&nbsp;   container\_name: mysql\_db

&nbsp;   environment:

&nbsp;     MYSQL\_ROOT\_PASSWORD: root

&nbsp;     MYSQL\_DATABASE: ivolve

&nbsp;     MYSQL\_USER: app

&nbsp;     MYSQL\_PASSWORD: 12345

&nbsp;   ports:

&nbsp;     - "3306:3306"

&nbsp;   volumes:

&nbsp;     - db\_mysql:/var/lib/mysql



volumes:

&nbsp; db\_mysql:

3- Run the Stack

bash

Copy code

docker-compose up -d

4- Verify Running Containers

bash

Copy code

docker ps

Expected output:



bash

Copy code

node-app   ...   0.0.0.0:3000->3000/tcp

mysql\_db   ...   3306/tcp

5- Verify the Application

Open in browser or use curl:



bash

Copy code

curl http://localhost:3000

curl http://localhost:3000/health

curl http://localhost:3000/ready

6- Check Application Logs

Logs are stored inside the container and mapped locally:



bash

Copy code

docker exec -it node-app ls /app/logs

or check from the host:



bash

Copy code

./logs/

7- Push the Docker Image to DockerHub

Login:



bash

Copy code

docker login

Build the image:



bash

Copy code

docker build -t your\_dockerhub\_username/node-app:latest .

Push it:



bash

Copy code

docker push your\_dockerhub\_username/node-app:latest



