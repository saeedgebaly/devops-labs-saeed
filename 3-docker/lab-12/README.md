Lab 12: Docker Volume and Bind Mount with Nginx
### Objective

In this lab, you will learn how to use Docker Volumes and Bind Mounts to persist data and serve files from the host machine using Nginx.

 Steps
### Create a Docker Volume

Create a volume named nginx_logs to persist Nginx log files.

docker volume create nginx_logs


Verify the volume:

docker volume ls


Inspect the volume to see its mount path:

docker volume inspect nginx_logs

### Create a Bind Mount Directory

Create a local directory to serve custom HTML content.

mkdir -p nginx-bind/html

### Create a Custom HTML File

Create an index.html file in your local directory:

echo "Hello from Bind Mount" > nginx-bind/html/index.html

### Run Nginx Container

Run an Nginx container using:

Volume for /var/log/nginx

Bind Mount for /usr/share/nginx/html

docker run -d \
  --name nginx-lab12 \
  -p 8080:80 \
  -v nginx_logs:/var/log/nginx \
  -v $(pwd)/nginx-bind/html:/usr/share/nginx/html \
  nginx

### Verify Nginx Page

Use curl to check the running Nginx page:

curl http://localhost:8080


Expected output:

Hello from Bind Mount

### Update the HTML File

Modify the file on your local machine:

echo "Hello again from Bind Mount (updated!)" > nginx-bind/html/index.html


Recheck the Nginx page:

curl http://localhost:8080


Expected output updates immediately (Bind Mount reflects changes live).

### Verify Logs Are Stored in Volume

Check that Nginx logs are saved inside the volume nginx_logs.

Run a temporary container to list files inside the volume:

docker run --rm -v nginx_logs:/data alpine ls /data


Expected output:

access.log
error.log


(These are the Nginx access and error log files.)

### Cleanup

Stop and remove the container:

docker stop nginx-lab12
docker rm nginx-lab12


Remove the volume:

docker volume rm nginx_logs