\# EC2 Auto Scaling



\## Objective



The objective of this exercise was to configure Amazon EC2 Auto Scaling so that EC2 instances could automatically increase or decrease based on workload.



\## 1. Launch Template



A Launch Template was created to define the configuration used when Auto Scaling launches new EC2 instances.



The template included:



\- Amazon Machine Image (AMI)

\- EC2 instance type

\- Key pair

\- Security group

\- Network configuration



\## 2. Auto Scaling Group



An Auto Scaling Group was created using the Launch Template.



\### Capacity Configuration



| Setting | Value |

|---|---:|

| Minimum capacity | 1 |

| Desired capacity | 2 |

| Maximum capacity | 4 |



The Auto Scaling Group was configured to use subnets across multiple Availability Zones.



\## 3. Scaling Policy



A scaling policy based on CPU utilization was configured.



The objective was to increase the number of EC2 instances when CPU utilization exceeded approximately 70%.



This allows the application to respond automatically to increased workload.



\## 4. Testing Auto Scaling



A CPU stress test was performed on an EC2 instance to generate additional workload.



The increased CPU utilization allowed the scaling policy to be tested.



The Auto Scaling Group was monitored through the EC2 console to observe changes in the number of running instances.



\## Result



The Auto Scaling Group successfully maintained two EC2 instances as the desired capacity and provided the ability to scale between one and four instances depending on workload.



\## What I Learned



This exercise demonstrated how EC2 Auto Scaling provides elasticity by automatically adjusting computing capacity according to application demand.



I also learned how Launch Templates, Availability Zones, and scaling policies work together to create a more resilient and scalable AWS environment.



