\# EC2 Spot Instances



\## Objective



The objective of this exercise was to explore Amazon EC2 Spot Instances and understand how they can be used as a cost-optimization option compared with On-Demand Instances.



\## 1. Launching a Spot Instance



An EC2 Spot Instance was launched using the AWS EC2 console.



The Spot purchasing option was selected during the instance configuration.



The instance was successfully launched and accessed for testing.



\## 2. Spot Instance Verification



The EC2 Instance Metadata Service was used to verify the purchasing model of the instance.



The following command was executed from the EC2 instance:



```bash

curl http://169.254.169.254/latest/meta-data/instance-life-cycle

The command returned:



spot



This confirmed that the EC2 instance was running as a Spot Instance.



3\. Spot vs. On-Demand



Spot Instances use unused EC2 capacity and can provide significant cost savings compared with On-Demand Instances.



However, Spot Instances can be interrupted when AWS needs the underlying capacity or when the Spot price exceeds the configured limit.



Feature	Spot Instance	On-Demand Instance

Cost	Lower	Higher

Availability	Can be interrupted	Generally available while running

Best use	Flexible workloads	Continuous workloads

Cost optimization	High	Lower

Result



A Spot Instance was successfully launched and verified.



The exercise demonstrated how Spot Instances can reduce AWS infrastructure costs for workloads that can tolerate interruptions.



What I Learned



This exercise helped me understand the difference between Spot and On-Demand EC2 purchasing models.



I learned that Spot Instances are useful for flexible and fault-tolerant workloads where temporary interruption is acceptable.



Examples include batch processing, testing, development environments, and other workloads that do not require uninterrupted operation.

