# Scalable_Wordpress_Deployment

This is a Word-press application deployment on multi-server that span across two Availability group.  deploy a highly available infrastructure that to prevent a single point of failure with hindsight for cost optimization. 
It is a three-tier architecture. The first tier is the public subnet, second tier is private subnet (Application Server) and Third is a Database Tier.

The architecture design is on AWS cloud platform specifically on AWS-EU-WEST-1 region. 
It has a Single VPC which provide the network infrastructure and it contains two subnets.
i.	Public subnet.
ii.	Private subnet.
1. Public subnet: - Application load balancer and Bastion host for administration are deployed here. Bastion Hosts use to send and receive traffic.  NAT gateway allow communication within the public subnet while. All resources or instance deployed here will have a public facing IP address that will be visible and accessible on the internet.  
INTERNET GATEWAY allow communication among all resources within the VPC and internet.
2. Private Subnet (Web/App subnet and Data subnet)
Web server is installed in the private subnet to prevent a direct access from outside world and this provides a form of security.
ELASTIC Cache cluster caches queried requests by users and speed up responses.  Amazon RDS is use as the WordPress database. Since this is a multi-server architecture all datafile that feeds to the WordPress server is shared on amazon EFS file system using EFS mount target.
 Amazon CloudFront:  A WEB Service that provide cost effective way to distribute web contents with low latency. Cache contents are downloaded close to end users for faster delivery. CloudFront pulls static contents from S3 bucket. it uses cache control headers to identify how long cache of http and https are cached for. Dynamic contents are accessed via Application Load Balancer
Database Caching: - Database caching can reduce latency and increase throughput for heavy application workloads.  Application performance is improved by storing frequently accessed pieces of data in memory for low-latency access 
Jenkins Server is installed on AWS Ec2 and it will pull the terraform code from GitHub. This will deploy the whole infrastructure on AWS, and it will be monitored by Prometheus and Grafana use to Visualise the Captured Metrics by Prometheus.
