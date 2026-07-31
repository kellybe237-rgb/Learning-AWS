
# AWS Cloud Internship – Week 1 Learning Journey 🚀

## Overview

During the first week of my AWS Cloud Internship, I gained hands-on experience with core AWS services and fundamental cloud computing concepts. I explored how cloud infrastructure works by launching virtual servers, configuring networking and security, deploying web servers, and creating reusable machine images.

---

## What I Learned

### 1. AWS Free Tier Account

* Created an AWS Free Tier account to begin working with cloud services.
* Learned that **Amazon Web Services (AWS)** is a cloud computing platform that allows individuals and organizations to deploy applications without purchasing or maintaining physical servers.
* Understood the benefits of cloud computing, including scalability, flexibility, and pay-as-you-go pricing.

---

### 2. Launching an Amazon EC2 Instance

* Launched an **Amazon EC2 Ubuntu Linux instance**.
* Learned that an EC2 instance is a virtual machine hosted in AWS that can be used to run applications, websites, and services.
* Became familiar with the EC2 launch process and basic instance management.

---

### 3. Configuring Security Groups

Configured security groups to control inbound traffic by opening only the required ports:

| Port | Protocol | Purpose                            |
| ---- | -------- | ---------------------------------- |
| 22   | SSH      | Secure remote access to the server |
| 80   | HTTP     | Serve web traffic                  |
| 443  | HTTPS    | Secure web traffic                 |

This helped me understand how AWS security groups function as virtual firewalls for EC2 instances.

---

### 4. Installing Web Servers

After launching the EC2 instance, I installed and configured:

* Apache2
* Nginx

I successfully verified both web servers by accessing the instance through its **public IPv4 address** using a web browser.

---

### 5. Deploying Applications with Amazon Lightsail

Created an **Amazon Lightsail** instance and deployed pre-configured applications, including:

* WordPress
* Node.js

I learned how Lightsail simplifies application deployment by providing ready-to-use development environments and accessed the deployed applications through the instance's public IP address.

---

### 6. Working with Elastic IP Addresses

* Created an **Elastic IP**.
* Associated the Elastic IP with my EC2 Linux instance.
* Verified that my web server remained accessible using the static public IP address.

This demonstrated the importance of Elastic IPs in maintaining a consistent public endpoint even if an instance is restarted.

---

### 7. Creating an Amazon Machine Image (AMI)

* Created an **Amazon Machine Image (AMI)** from my configured EC2 instance.
* Launched a new EC2 instance using the AMI.

This showed me how AMIs can be used to quickly replicate configured environments, making deployments faster and more consistent.

---

## Skills Gained

* AWS Free Tier
* Amazon EC2
* Ubuntu Linux
* Security Groups
* Apache2
* Nginx
* Amazon Lightsail
* Elastic IP
* Amazon Machine Image (AMI)
* Basic Cloud Infrastructure
* Web Server Deployment

---

## Key Takeaways

This first week provided a strong foundation in AWS cloud computing. I learned how to provision virtual servers, secure network access, deploy web applications, assign static IP addresses, and create reusable machine images. These practical exercises strengthened my understanding of cloud infrastructure and prepared me for more advanced AWS services and real-world deployments in the coming weeks.

**Looking forward to expanding my AWS knowledge and building more cloud-based solutions throughout the internship.** ☁️
