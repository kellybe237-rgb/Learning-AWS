\# Docker Deployment on EC2



\## Objective



The objective was to explore containerization by deploying a web server inside a Docker container on an EC2 instance.



\## Steps Completed



\### 1. Install Docker



Docker was installed on the EC2 instance.



The installation was verified using:



```bash

docker --version



The Docker service was started and enabled.



sudo systemctl start docker

sudo systemctl enable docker



The Apache HTTP Server image was downloaded from Docker Hub:

sudo docker pull httpd:latest



A custom index.html file was created containing the web content.

The Apache container was started and port 80 was mapped to the EC2 instance:



sudo docker run -d -p 80:80 httpd:latest



The running containers were checked using:



sudo docker ps



The Apache web server successfully ran inside a Docker container on the EC2 instance. The web page could be accessed through the EC2 public address.



What I Learned



This exercise demonstrated how Docker can package and run applications in isolated containers. I also learned how container ports can be mapped to EC2 ports to make a containerized web application accessible to users.







