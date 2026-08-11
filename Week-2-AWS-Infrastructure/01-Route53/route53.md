\# Amazon Route 53



\## Objective



The objective of this exercise was to configure Amazon Route 53 for DNS management, health monitoring, failover, and traffic distribution.



\## 1. Health Checks



A Route 53 health check was created to monitor the availability of an EC2 web server.



The health check was configured to monitor the server using HTTP.



The health check allowed the availability of the web server to be monitored and used as part of a highly available DNS configuration.



\## 2. Failover Routing



A primary and secondary EC2 instance were configured for DNS failover.



The primary instance handled normal traffic, while the secondary instance was configured as the backup resource.



The failover configuration allowed Route 53 to direct traffic to the secondary instance if the primary resource became unavailable.



\### Architecture



```text

&#x20;                Route 53

&#x20;                   |

&#x20;         +---------+---------+

&#x20;         |                   |

&#x20;         v                   v

&#x20;     Primary EC2         Secondary EC2

&#x20;     (Primary)             (Failover)



Weighted routing was used to distribute traffic between two EC2 instances.



The following weights were configured:



Instance	Weight

Instance A	70%

Instance B	30%



This configuration demonstrated how Route 53 can distribute DNS traffic between multiple resources.



4\. Domain Configuration



The domain gamersco.org was also configured during the AWS exercises.



Route 53 was later integrated with CloudFront so that the domain could use HTTPS.



The final DNS path for the CloudFront configuration was:



gamersco.org

&#x20;     |

&#x20;     v

&#x20;  Route 53

&#x20;     |

&#x20;     v

&#x20; CloudFront

Result



The Route 53 exercises successfully demonstrated DNS management, health checks, failover routing, and weighted traffic distribution.



These features can improve application availability and provide different methods for managing traffic between cloud resources.



What I Learned



This exercise helped me understand that Route 53 is more than a basic DNS service. It can also monitor resource health and make routing decisions based on health status and configured routing policies.



I learned how health checks, failover routing, and weighted routing can be used to build more reliable and flexible AWS architectures.



