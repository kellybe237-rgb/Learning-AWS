\# Application Load Balancer



\## Objective



The objective of this exercise was to deploy an Application Load Balancer (ALB) and use it to distribute web traffic between multiple EC2 instances.



\## 1. Create the Application Load Balancer



An internet-facing Application Load Balancer was created through the Amazon EC2 console.



The load balancer was configured with:



\- Load balancer type: Application Load Balancer

\- Scheme: Internet-facing

\- Listener: HTTP

\- Port: 80

\- Availability Zones: Multiple Availability Zones

\- Security group: Configured to allow HTTP traffic



\## 2. Target Group



A target group was created for the web servers.



The target group used:



\- Target type: Instances

\- Protocol: HTTP

\- Port: 80

\- Health check protocol: HTTP



Two EC2 instances were registered as targets.



The target group health checks were used to verify that the EC2 instances were available to receive traffic.



\## 3. Web Server Configuration



The two EC2 instances were configured with different web content so that traffic distribution could be observed.



For example:



```text

Server A

and:



Server B



This made it possible to identify which EC2 instance responded to a request.



4\. Testing the Load Balancer



After the targets became healthy, the DNS name provided by the Application Load Balancer was opened in a web browser.



The ALB successfully forwarded requests to the registered EC2 instances.



Architecture

&#x20;                 User

&#x20;                   |

&#x20;                   v

&#x20;         Application Load

&#x20;             Balancer

&#x20;                   |

&#x20;            Target Group

&#x20;             /         \\

&#x20;            /           \\

&#x20;           v             v

&#x20;      EC2 Server A   EC2 Server B

5\. Health Checks



The ALB continuously used health checks to determine whether the registered EC2 instances were available.



Only healthy targets were used to serve application traffic.



This provided an additional level of reliability because traffic could be directed away from an unhealthy instance.



Result



The Application Load Balancer successfully distributed HTTP traffic between the two EC2 instances.



The ALB DNS name provided a single endpoint through which users could access the application.



What I Learned



This exercise demonstrated how an Application Load Balancer can distribute traffic across multiple EC2 instances.



I learned how listeners, target groups, health checks, and Availability Zones work together to improve application availability and scalability.



The exercise also showed why load balancers are useful when applications need to support multiple backend servers.

