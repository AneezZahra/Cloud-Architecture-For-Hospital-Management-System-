# Cloud-Architecture-For-Hospital-Management-System-
Cloud Architecture For Hospital Management System 

Your tasks
Present the proposed solution to the customer in the form of a professional report. Within the report, include the following:
TASK 1: Translate customer requirements into a proposed technical solution. Identify the key AWS Services required and justify the need for each based on the detailed technical requirements above. Ensure that you articulate how each will be used to solve Medi- Advices needs.

Answer: Current environment of Medi advice is deployed in on-premises data center which is over provisioned and is not suitable for the company. Following are the issues in current environment:
1.	Database is not redundant and scalable or in technical terms we consider the database as bottle neck. If there is any issue or disruption, your system stops till the issue is not solved. There is no any other database server which will take over in case of failure. whole system will go down until you fix the current and only data base server.
2.	Whole system is slow, unable to handle traffic 
3.	If there is a disruption in one region the application has cross-region disaster recovery

In order to achieve highest performance and most effective cloud solution we will use Amazon web services. Our Web application architecture is spanning two availability zones. The idea behind two zones is that there is also a big demand for the application both in Ireland and in the US. So, one region should be nearest to Ireland and the other should be nearest to US users, make them easy access to reach the resources. In addition to that, both of these regions are connected by a VPN Connector through Gateways on the ends. This is because if there is any problem in one region to access the data, traffic will be directed to other region. One region can act as backup to other.
 This architecture is based on on-demand billing option for Ec2 instances. We will not use reserved instances to avoid any additional cost. Following are the AWS services that we will use:
1.	Route 53
Users DNS requests are served by route 53, which is highly available
For Medi advice we will use:
•	1 hosted zone
•	Up to 1 million quires

2.	Load balancer
Incurrent scenario of Medi advice, the system is very slow to respond to changes with their resource needs. If there is a demand in traffic, a technical services member will need to manually boot a machine. In order to resolve this issue, we will use Amazon load balancer. HTTP requests are handled by elastic load balancer which automatically distributes incoming traffic among the servers running the applications.
Specifications of Load balancer will be:
•	Data processing capacity = 50 GB

3.	Auto scaling group
Medi-Advice are a start-up, so we will use cost optimize services and will eliminate unneeded expenses. The web and application tiers will be deployed in AWS autoscaling group which automatically adjusts compute capacity up and down to handle the incoming load and also autoscaling is a free service.

4.	Web and application servers
Web and application services are hosted on amazon EC2 instances which are deployed within auto scaling groups
Ec2 servers required for current architecture servers:
Web application server = 2 Ec2 Linux instances
Web application servers = 2 Ec2 Linux instances
To create amazon instances, we will use Amazon machine images AMIs. For web and application tiers we will use (m1. Small) windows instance running with 100% utilization with on demand billing. 

5.	Amazon VPC 
We will use a Virtual private cloud for our architecture which is free of cost. 

6.	EBS
Attached to these EC2 instances we will use Elastic Block Storage volume to support these instances, for both throughput and transaction intensive workloads at any scale.
4 standard volumes
300GB
100 IOPS
10% change daily snapshots (snapshots we have to pay for only incremental change)

7.	Elastic IP addresses
Elastic IP addresses exists independently of Ec2 instances, they can be attached to the instance’s public facing IP addresses. Public IP addresses are free. Static IP address is assigned to an EC2 instance automatically and changes when you stop and run the instance again for any purpose. On the other side, elastic IP address is assigned by user and which does not change on restarting the instance.
For our architecture we will use:
1 Elastic IP address
10 remaps/month

8.	Relational Database Service
Persistent tiers are managed through amazon relational database service. RDS makes it easy to setup, operate and scale through relational database in the cloud while automating management and time-consuming administration tasks. We will use multi -A-Z mirrored slave failover to assure high availability.
For our architecture We will use:
2 db.m1.small (MySQL)
Running 100% utilized
20 GB storage
Multi-AZ mirrored slave failover

9.	Dynamo DB:
Application tier can store file meta data and unique identifiers in amazon dynamo DB which is a fast and fully managed NoSQL data base service that can store and retrive any amount of data and serve any level of request traffic
Dynamo DB usage parameters We will use:
Data Set size: 20 GB
Record size 1KB
Read/ Sec: 500
Writes/sec : 100
Data Transfer out : 50 GB/month

10.	Amazon S3
For resources and static content used by web application will be stored on Amazon simple storage service.
For this architecture we will use:
Storage 30GB
Data transfer out: 300 GB
Data transfer In: 30 GB
Put requests 10000
Get requests 100000

11.	AWS Elemental Media Convert
In Medi-Advice the application allows patients to upload documents and images. Text is extracted from documents, and images are converted into multiple formats. which is currently a manual process to automate this process we will use Amazon Elemental Mediacovert

12.	Cloud front
For static and streaming content, we will use amazon cloud front, a global content distribution network consisting of age locations that automatically route traffic for the best possible performance. Cloud front is a cross region service
For this architecture we will use:
Outbound volume: 300 GB/month
Avg object size: 300 KB
Traffic distrib : 100 % USA ( all contents being served from edge locations within the united states.

13.	VPN connector
This is to connect the two VPN regions, if there is any problem in one region, the users from that region will be directed to another region to remove the issue which was facing due to not redundant database.




TASK 2: Create an architecture diagram(s) of the proposed solution to meet Medi-Advices needs. Design an AWS solution meeting the requirements provided by the customer. Using a tool such as draw.io (https://app.diagrams.net/?splash=0&libs=aws4). Ensure to articulate the highly available architecture design needs of Medi-Advice and their cross- region design
Ans:
Note: This architecture is for N.California region . We have to replicate the same architecture in another region i.e.  for EU(Ireland) we will use eu-wes1 and eu-east1 zones. We will connect both regions using AWS VPN connect having gateways on its end. This is to make the region available for the people if one region goes down due to any issue. i.e. if N.California region has any problem and it goes down, the customers from this region will be directed to EU region.

 






TASK 3*: Implement a proof-of-concept solution demonstrating configuring and testing of a cross-region disaster recovery scenario. Test the failover to your secondary web server if a primary web server fails. Use print screens to showcase this work. Briefly outline why implementing a solution like this would-be beneficial to Medi-Advices needs.

 


TASK 4: a) Ensure to discuss TWO anti-patterns that Medi-Advice currently have. Clearly explain the problems and justify how your solution would solve these two anti-patterns.
Current environment of Medi advice is deployed in on-premises data center which is over provisioned and is not suitable for the company. Following are the issues in current environment:
1.	Database is not redundant and scalable. There is no any other database server which will take over in case of failure. whole system will go down until you fix the current and only data base server.
2.	Whole system is slow, unable to handle traffic. As their database is in Dublin city and its not closest to both the locations (Ireland and US)


        Solution:
1.	The architecture we provided has a redundancy for the database. There are two redundant database we are using, one in each region. If there is a disruption in one region the application has cross-region disaster recovery, we direct the user to another region.
2.	Secondly system was slow and unable to handle traffic or large number of users. Our system has the property of autoscaling the resources. If there is more traffic, it will automatically fix the quantity of resources need by scaling up and vise versa. One of reason for the slowness is that the database was far from the user and all the users were relying on the only database. We are bringing the database locations to the nearest points for the premises.

b. ) Finally, conclude your report by discussing ways how Medi-Advice can optimize the cost of their AWS infrastructure.

Medi-Advice are a start-up, so we will use cost optimize services and will eliminate unneeded expenses. The web and application tiers will be deployed in AWS autoscaling group which automatically adjusts compute capacity up and down to handle the incoming load , so Medi advice will be charged only when the resources are used and also autoscaling is a free servics 
References
https://aws.amazon.com/ec2/?ec2-whats-new.sort-by=item.additionalFields.postDateTime&ec2-whats-new.sort-order=desc

https://aws.amazon.com/route53/

https://aws.amazon.com/cloudfront/streaming/
https://aws.amazon.com/autoscaling/

