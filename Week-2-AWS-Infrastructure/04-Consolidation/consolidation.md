\# AWS Hands-On Consolidation



\## Objective



The objective of this exercise was to combine Amazon Route 53, an Application Load Balancer (ALB), and EC2 Auto Scaling into one scalable and highly available AWS architecture.



\## 1. Auto Scaling Group



An Auto Scaling Group was configured to manage the EC2 web servers.



The capacity settings were:



| Setting | Value |

|---|---:|

| Minimum capacity | 1 |

| Desired capacity | 2 |

| Maximum capacity | 4 |



The instances were deployed across multiple Availability Zones.



\## 2. Application Load Balancer



The Application Load Balancer was configured to distribute incoming HTTP requests across the EC2 instances managed by the Auto Scaling Group.



The ALB used a target group to register and monitor the EC2 instances.



Health checks were configured to ensure that only healthy instances received traffic.



\## 3. Route 53



Route 53 was used to provide DNS access to the application.



The domain `gamersco.org` was used during the AWS exercises.



The DNS configuration allowed the domain to be associated with the application infrastructure.



\## 4. Combined Architecture



The services were combined into the following architecture:



```text

&#x20;                   User

&#x20;                     |

&#x20;                     v

&#x20;                Route 53

&#x20;                     |

&#x20;                     v

&#x20;           Application Load

&#x20;               Balancer

&#x20;                     |

&#x20;                     v

&#x20;               Target Group

&#x20;                     |

&#x20;            +--------+--------+

&#x20;            |                 |

&#x20;            v                 v

&#x20;          EC2 A             EC2 B

&#x20;            ^                 ^

&#x20;            |                 |

&#x20;            +--------+--------+

&#x20;                     |

&#x20;              Auto Scaling

&#x20;               Group



5\. Auto Scaling and Load Balancing



The Auto Scaling Group was connected to the ALB target group.



This allowed instances launched by the Auto Scaling Group to become available to the load balancer.



If an EC2 instance became unhealthy, the ALB health check could identify the problem and stop sending traffic to that instance.



Auto Scaling could then maintain the required capacity by launching a replacement instance when necessary.



6\. Testing



The application was accessed through the load balancer endpoint.



The EC2 instances were configured with different web content to verify that traffic was being distributed between the servers.



CPU utilization was also increased during testing to demonstrate the Auto Scaling functionality.



Result



The AWS services successfully worked together to create a scalable and highly available web application architecture.



Route 53 provided DNS management, the Application Load Balancer distributed application traffic, and EC2 Auto Scaling automatically managed the number of running instances.



What I Learned



This exercise demonstrated the importance of combining AWS services rather than relying on a single service.



Using Route 53, an ALB, and Auto Scaling together provides better availability, scalability, and fault tolerance than using a single EC2 instance.



The exercise also helped me understand how load balancing and automatic scaling complement each other in a cloud environment.

