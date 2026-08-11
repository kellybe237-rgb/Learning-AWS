\# Amazon CloudFront, ACM and Lambda@Edge



\## Objective



The objective of this exercise was to explore Amazon CloudFront, AWS Certificate Manager (ACM), HTTPS, and Lambda@Edge as advanced AWS services for secure and efficient web application delivery.



\## 1. AWS Certificate Manager



A public SSL/TLS certificate was requested through AWS Certificate Manager (ACM).



The certificate was created for:



```text

gamersco.org



DNS validation was selected as the validation method.



A CNAME validation record was added to the Route 53 hosted zone.



After successful DNS validation, the certificate status changed to:



Issued



The certificate was created in the US East (N. Virginia) region because CloudFront requires ACM certificates to be available in this region.



2\. CloudFront Distribution



A CloudFront distribution was created to provide content delivery and HTTPS access.



The Application Load Balancer was configured as the CloudFront origin.



The configuration included:



Origin: Application Load Balancer

Alternate domain name: gamersco.org

SSL/TLS certificate: ACM certificate

Viewer protocol policy: Redirect HTTP to HTTPS

HTTP origin connection to the ALB

3\. Route 53 Integration



The Route 53 A record for gamersco.org was changed from the EC2/ALB destination to an Alias record pointing to the CloudFront distribution.



The resulting traffic path was:



User

&#x20;|

&#x20;| HTTPS

&#x20;v

gamersco.org

&#x20;|

&#x20;v

Route 53

&#x20;|

&#x20;v

CloudFront

&#x20;|

&#x20;| HTTP

&#x20;v

Application Load Balancer

&#x20;|

&#x20;v

EC2 Instances

4\. HTTPS Testing



The domain was tested through a web browser using:



https://gamersco.org



The website loaded successfully over HTTPS.



HTTP requests were configured to redirect to HTTPS through the CloudFront viewer protocol policy.



5\. Lambda@Edge



A Lambda function was created to explore Lambda@Edge functionality.



The function was designed to modify an HTTP response by adding a custom response header:



X-Edge-Demo: Lambda-at-Edge



Lambda@Edge allows Lambda functions to run in association with CloudFront and process requests or responses closer to users.



The conceptual architecture was:



User

&#x20;|

&#x20;v

Route 53

&#x20;|

&#x20;v

CloudFront

&#x20;|

&#x20;v

Lambda@Edge

&#x20;|

&#x20;v

Application Load Balancer

&#x20;|

&#x20;v

EC2

6\. Security



The CloudFront configuration provided HTTPS encryption between the user's browser and CloudFront.



AWS Certificate Manager was used to manage the SSL/TLS certificate, reducing the need to manually manage certificates on the web server for this configuration.



Result



CloudFront was successfully integrated with Route 53, ACM, and the Application Load Balancer.



The domain gamersco.org was successfully accessed using HTTPS.



The exercise also introduced Lambda@Edge and demonstrated how edge computing can be integrated with CloudFront.



What I Learned



This exercise demonstrated how AWS services can be combined to provide secure and efficient web application delivery.



I learned how ACM certificates can be used with CloudFront, how Route 53 can direct domain traffic to CloudFront, and how CloudFront can provide HTTPS access and content delivery.



I also gained an understanding of Lambda@Edge and how serverless functions can be associated with CloudFront for edge-based processing.

