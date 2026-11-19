## Architecture 2 – AWS EKS Cloud.
## Presentation.

For cloud architecture, I recommend Amazon EKS with a multi-AZ deployment.
# Presentation.

You should explain how your architecture will handle 25,000 users, avoid latency, distribute traffic, scale microservices, maintain high availability and control infrastructure costs.

<img width="940" height="356" alt="image" src="https://github.com/user-attachments/assets/40644662-43a2-4a93-af40-3dd190b74410" />


## What does seamless mean?
Seamless means users should not notice what is happening behind the scenes, even when thousands of other users are accessing the application.
For example:
•	1,000 users access the application. Suddenly, traffic increases to 25,000 users.
•	Load balancer distributes traffic across healthy application instances.
•	Kubernetes increases the number of pods when required.
•	If one pod or server fails, traffic moves to healthy instances.
Users should not experience application downtime or major performance degradation.
## Solution:
HPA will scale the application pods, and Karpenter will provision additional EC2 worker nodes when existing capacity is insufficient.


## low latency.
For low latency, we will use CloudFront, Redis caching, database optimization and compression.

<img width="901" height="377" alt="image" src="https://github.com/user-attachments/assets/9d78429a-19e5-4088-89dc-24fee83a6458" />


## How can we reduce egress costs?

1. CloudFront CDN.
Cache static files and reusable datasets near users. Reduce repeated requests to the application origin.

2. S3 for large datasets
Store large files in S3 instead of transferring everything through application pods. Serve eligible objects through CloudFront.

3. Redis caching.
Store frequently accessed application data in Redis. This reduces repeated database queries and backend processing.

## 6. How do we handle high data transfer and high bandwidth?
If the application transfers large images, maps, videos or datasets, do not route every large file through Kubernetes pods.
Proposed flow:
User → CloudFront → S3.


## Requirement.              Solution.

Large images and maps	       S3
Fast content delivery	       CloudFront
Frequently accessed data	   Redis
Network capacity	           Proper EC2 network performance and load testing





![Uploading image.png…]()



