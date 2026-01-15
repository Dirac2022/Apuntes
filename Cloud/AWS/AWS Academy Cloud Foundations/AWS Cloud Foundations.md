
# Cloud Concepts Overview


# Cloud Economics and Billing


# AWS Global Infrastructure Overview

## AWS Global Infrastructure

The **AWS Global Infrastructure** is designed and built to deliver a flexible, reliable, scalable, and secure cloud computing environment with high-quality global network performance.

This map shows the current **AWS Regions** and more that are coming soon

![d88d2fecf52142786da539be437e50df_d-11-f-53-af-b-76-f-482-d-8492-73-be-2-a-630-f-1-b.png (837×487)](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/aws-cloud-technical-professionals/explore-the-aws-global-infrastructure-technical-professionals/images/d88d2fecf52142786da539be437e50df_d-11-f-53-af-b-76-f-482-d-8492-73-be-2-a-630-f-1-b.png)


### AWS Regions

An **AWS Region** is a geographical area.

- An AWS region is a physical geographical location with one or more Availability Zones.
- An Availability Zone in turn consists of one or more data centers.
- To achieve fault tolerance and stability AWS regions are isolated from one another.
- Resources in one region are not automatically replicated to another region.
- It is your responsibility to replicate data across regions if your business or project need require i
- Each Region provides full redundancy and connectivity to the network.

<h5>Selecting a Region</h5>
- Data governance, legal requirements
- Proximity to customers (latency)
- Services available within the Region
- Cost (vary by Region)

Currently 37 Regions and 117 Availability Zones: [Infraestructura global - AWS](https://aws.amazon.com/es/about-aws/global-infrastructure/)

### Availability Zones

- Each **Region** has multiple Availability Zones.
- Each **Availability Zone** is fully isolated partition of the AWS infrastructure.
	- Availability Zones consist fo discrete **data centers**
	- They are designed for fault isolation
	- They are interconnected with other Availability Zones by using high-speed private networking.

>[!tip]
>AWS recommends replicating data and resources across Availability Zones for resiliency





### AWS data centers

An Availability Zone is the most granular level of specification that a customer can make. However, a data center is the location where the actual data resides. 

- AWS data centers are designed for security.
- Data centers are where the data resides and data processing occurs.
- Each data center has redundant power, networking, and connectivity, and is housed in a separate facility
- A data center typically has 50 000 to 80 000 physical servers.



Data centers are securely designed with several factors in mind:

Each location is carefully evaluated to mitigate environmental risk.

- Data centers have a redundant design that anticipates and tolerates failure while maintaining service levels.
	
- To ensure availability, critical system components are backed up across multiple Availability Zones.
	
- To ensure capacity, AWS continuously monitors service usage to deploy infrastructure to support availability commitments and requirements.
	
- Data center locations are not disclosed and all access to them is restricted.
	
- In case of failure, automated processes move data traffic away from the affected area.



### Points of Presence

- AWS privides a global network of 187 **Points of Presence** locations
- Consist of 176 **edge locations** and 11 **Regional edge caches**.
- Used with Amazon CloudFront

Amazon **CloudFront** is a content delivery network (CDN) used to distribute content to end users to reduce latency. 

Amazon Route 53 is a Domain Name System (DNS) service. Requests going to either one of these services will be routed to the nearest edge location automatically in order to lower latency.AWS 

Regional edge caches are used by default with Amazon CloudFront. Regional edge caches are used when you have content that is not accessed frequently enough to remain in an edge location. Regional edge caches absorb this content and provide an alternative to that content having to be fetched from the origin server

### AWS infrastructures features

- Elasticity and scalability
- Fault-tolerance
- High availability


> [!tip]
> - **Edge Locations**: Small AWS data centers in major cities that deliver cached content closer to users with low latency.  
> Example: A user in Lima loads a website hosted in Virginia; thanks to an Edge Location in Lima or Santiago, the content is served locally instead of traveling to the U.S.
>
>
>- **Regional Edge Caches**: Larger caches that sit between Edge Locations and AWS Regions, helping reduce trips to the origin.  
> Example: If the file is not in Lima’s Edge Location, it may be found in the Regional Edge Cache in São Paulo before going back to Virginia.



## AWS services and service category overview

The AWS infrastructure provides the platform for a broad set of services, such as networking, storage, compute services, and databases.

![prMsfbj.png (1301×596)](https://i.imgur.com/prMsfbj.png)



![S1ZnF8g.png (1371×620)](https://i.imgur.com/S1ZnF8g.png)

AWS offers a broad set of cloud-based services. There are 23 different product or service categories, and each category consists of one or more services. 

The categories that this course will discuss are highlighted on the slide: Compute, Cost Management, Database, Management and Governance, Networking and Content Delivery, Security, Identity, and Compliance, and Storage.

### Storage service category

**Amazon Simple Storage Service (Amazon S3)** is an object storage service that offers scalability, data availability, security, and performance. Use it to store and protect any amount of data for websites, mobile apps, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics. 

**Amazon Elastic Block Store (Amazon EBS)** is high-performance block storage that is designed for use with Amazon EC2 for both throughput and transaction intensive workloads. It is used for a broad range of workloads, such as relational and non-relational databases, enterprise applications, containerized applications, big data analytics engines, file systems, and media workflows.

**Amazon Elastic File System (Amazon EFS)** provides a scalable, fully managed elastic Network File System (NFS) file system for use with AWS Cloud services and on-premises resources. It is built to scale on demand to petabytes, growing and shrinking automatically as you add and remove files. It reduces the need to provision and manage capacity to accommodate growth.

**Amazon Simple Storage Service Glacier** is a secure, durable, and extremely low-cost Amazon S3 cloud storage class for data archiving and long-term backup. It is designed to deliver 11 9s of durability, and to provide comprehensive security and compliance capabilities to meet stringent regulatory requirements.


### Compute service category

**Amazon Elastic Compute Cloud (Amazon EC2)** provides resizable compute capacity as virtual machines in the cloud. 

**Amazon EC2 Auto Scaling** enables you to automatically add or remove EC2 instances according to conditions that you define. 

**Amazon Elastic Container Service (Amazon ECS)** is a highly scalable, high-performance container orchestration service that supports Docker containers. 

**Amazon Elastic Container Registry (Amazon ECR)** is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images. 

**AWS Elastic Beanstalk** is a service for deploying and scaling web applications and services on familiar servers such as Apache and Microsoft Internet Information Services (IIS). 

**AWS Lambda** enables you to run code without provisioning or managing servers. You pay only for the compute time that you consume. There is no charge when your code is not running.

**Amazon Elastic Kubernetes Service (Amazon EKS)** makes it easy to deploy, manage, and scale containerized applications that use Kubernetes on AWS.

**AWS Fargate** is a compute engine for Amazon ECS that allows you to run containers without having to manage servers or clusters.

### Database service category

**Amazon Relational Database Service (Amazon RDS)** makes it easy to set up, operate, and scale a relational database in the cloud. It provides resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching, and backups. 

**Amazon Aurora** is a MySQL and PostgreSQL-compatible relational database. It is up to five times faster than standard MySQLdatabases and three times faster than standard PostgreSQL databases.

**Amazon Redshift** enables you to run analytic queries against petabytes of data that is stored locally in Amazon Redshift, and directly against exabytes of data that are stored in Amazon S3. It delivers fast performance at any scale.

**Amazon DynamoDB** is a key-value and document database that delivers single-digit millisecond performance at any scale, with built-in security, backup and restore, and in-memory caching.

### Networking and content delivery service category


**Amazon Virtual Private Cloud (Amazon VPC)** enables you to provision logically isolated sections of the AWS Cloud. 

**Elastic Load Balancing** automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions.

**Amazon CloudFront** is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and application programming interfaces (APIs) to customers globally, with low latency and high transfer speeds.

**AWS Transit Gateway** is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway. 

**Amazon Route 53** is a scalable cloud Domain Name System (DNS) web service designed to give you a reliable way to route end users to internet applications. It translates names (like [www.example.com](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/mitch/Documents/Proyecto%20Abogados%20-%20Luis%20Aza%C3%B1a/Programa/www.example.com)) into the numeric IP addresses (like 192.0.2.1) that computers use to connect to each other. 

**AWS Direct Connect** provides a way to establish a dedicated private network connection from your data center or office to AWS, which can reduce network costs and increase bandwidth throughput.

**AWS VPN** provides a secure private tunnel from your network or device to the AWS global network. 

### Security, identity, and compliance service category

**AWS Identity and Access Management (IAM)** enables you to manage access to AWS services and resources securely. By using IAM, you can create and manage AWS users and groups. You can use IAM permissions to allow and deny user and group access to AWS resources. 

**AWS Organizations** allows you to restrict what services and actions are allowed in your accounts. 

**Amazon Cognito** lets you add user sign-up, sign-in, and access control to your web and mobile apps.

**AWS Artifact** provides on-demand access to AWS security and compliance reports and select online agreements. 

**AWS Key Management Service (AWS KMS)** enables you to create and manage keys. You can use AWS KMS to control the use of encryption across a wide range of AWS services and in your applications. 

**AWS Shield** is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS.

### AWS cost management service category


The **AWS Cost and Usage Report** contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations.

**AWS Budgets** enables you to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount.

**AWS Cost Explorer** has an easy-to-use interface that enables you to visualize, understand, and manage your AWS costs and usage over time.

### Magagement and governance service category

The **AWS Management Console** provides a web-based user interface for accessing your AWS account.

**AWS Config** provides a service that helps you track resource inventory and changes.

**Amazon CloudWatch** allows you to monitor resources and applications.

**AWS Auto Scaling** provides features that allow you to scale multiple resources to meet demand.

**AWS Command Line Interface** provides a unified tool to manage AWS services.

**AWS Trusted Advisor** helps you optimize performance and security.

**AWS Well-Architected Tool** provides help in reviewing and improving your workloads.

**AWS CloudTrail** tracks user activity and API usage.


# AWS Cloud Security


# Networking and Content Delivery

[[Lab 2 Build your VPC and Launch a Web Server]]


# Compute

[[Lab 3 Introduction to Amazon EC2]]
## Compute services overview

![1*8_jlyMlLsWJQ8WjOYkLVow.png (986×572)](https://miro.medium.com/v2/resize:fit:1400/1*8_jlyMlLsWJQ8WjOYkLVow.png)


<h5Categorizing compute services</h5>

| Services                                                                    | Key Concepts                                                                         | Characteristics                                                                                                                       |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Amazon EC2**                                                              | - Infrastructure as a service (IaaS) <br> - Instance-based <br> - *Virtual machines* | - Provision virtual machines that you can manage as you choose                                                                        |
| **AWS Lambda**                                                              | - *Serverless* computing <br> - Function-based <br> - Low-cost                       | - Write and deploy code that runs on a schedule or that can be triggered by events <br> - Use when possible (architect for the cloud) |
| **Amazon ECS** <br> **Amazon EKS** <br> **AWS Fargate** <br> **Amazon ECR** | - *Container-based* computing <br> - Instance-based                                  | - Spin up and run jobs more quickly                                                                                                   |
| **AWS Elastic Beanstalk**                                                   | - Platform as a service (PaaS) <br> - For *web applications*                         | - Focus on your code (building your application) <br> - Can easily tie into other services—databases, Domain Name System (DNS), etc.  |


<h5>Choosing the optimal compute service</h5>
Some aspects to consider
- What is your application design?
- What are your usage patterns?
- Which configuration settings will you want to manage?

Selecting the wrong compute solution for an architecture can lead to lower performance efficiency
- A good starting place: Understand the available compute options



## Amazon EC2

Amazon Elastic Compute Cloud (Amazon EC2) provides virtual machines where you can host the same kinds of applications that you might run on a traditional on-premises server. It provides secure, resizable compute capacity in the cloud. Common uses for EC2 instances include, but are not limited to:
- Application servers•Web servers
- Database servers•Game servers
- Mail servers•Media servers
- Catalog servers
- File servers
- Computing servers
- Proxy servers

**Amazon Elastic Compute Cloude (Amazon EC2)**
- Provides virtual machines, referred to as **EC2 instances**, in the cloud.
- Gives you full control over the guest operating system (Window, Linux, etc.) on each instance.

**You can launch instances of any size into an Availability Zone anywhere in the world**
- Launch instances from **Amazon Machine Images (AMI)**, which are effectively virtual machine templates.
- Launch instances with a few clicks or a line of code, and they are ready in minutes.

**You can control traffic to and from instances**



## Amazon EC2 cost optimization


## Container services






## Introduction to AWS Lambda


## Introduction to AWS Elastic Beanstalk




# Storage

[[Lab 4 Working with EBS]]
## Amazon Elastic Block Store (Amazon EBS)

Amazon EBS provides persistent block storage volumes for use with Amazon EC2 instances.

Each Amazon EBS volume is automatically replicated withing its Available Zone to protect you from component failure.

<h5>AWS storage options: Block storage versus object storage</h5>

![303f80268de68a20dea5c59d6dd04624_628906-ec-3-a-52-4092-b-37-c-fb-936-f-44-db-82.png (1386×716)](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/aws-storage/explore-aws-storage-types/images/303f80268de68a20dea5c59d6dd04624_628906-ec-3-a-52-4092-b-37-c-fb-936-f-44-db-82.png)

- With block storage, you change only the block that contains the character.
- With object storage, the entire file must be updated.

Block storage solutions are typically faster and use less bandwidth, but they can cost more than object-level storage.

### Amazon EBS

Amazon EBS enables you to **create individual storage volumes** and **attach them** to an Amazon EC2 instance.
- Amazon EBS offers block-level storage
- Volumes are automatically replicated within its Availability Zone.

EBS can be used to run a database with a n Amazon EC2 instance. Amazon EBS volumes are included as part of the backup of your instances into Amazon Machine Images. AMIs are store in Amazon S3 and can be reused to create new EC2 instances later.

A backup of an Amazon EBS volume is called a **snapshot**. The first snapshot is called the **baseline snapshot**. Any other snapshot after the baseline captures only what is different from the previous snapshot.

Uses:
- Boot volumes and storage for Amazon EC2 instances
- Data storage with a file system
- Database host
- Enterprise applications


<h5>Amazon EBS volume types</h5>

| Solid State Drives (SSD) |                  | Hard Disk Drives (HDD) |           |
| ------------------------ | ---------------- | ---------------------- | --------- |
| General Purpose          | Provisioned IOPS | Throughput-Optimized   | Cold      |
| 16 TiB                   | 16 TiB           | 16 TiB                 | 16 TiB    |
| 16,000                   | 64,000           | 500                    | 250       |
| 250 MiB/s                | 1,000 MiB/s      | 500 MiB/s              | 250 MiB/s |


Only SSDs can be used as boot volumes for EC2 instances.


### Amazon EBS features

**Snapshots**
To provide an even higher level of data durability, Amazon EBS enables you to create **point-in-time** snapshots of your volumes, and you can re-create a new volume from a snapshot at any time.

You can share snapshots or even copy them to different AWS Regions for even greater **disaster recovery (DR) protection**.

**Encryption**
- Encrypted Amazon EBS volumes
- No additional cost

**Elasticity**
- Increase capacity
- Change to different types. For example: From HDDs to SSDs.

### Amazon EBS: Volumes, IOPS, and pricing

When you begin to estimate the cost for Amazon EBS, you must consider the following:


**Volumes**

- Amazon EBS volumes persist independently from the instance.
- All volume types are charged by the amount that is provisioned per month.

**IOPS**
- General Purpose SSD: charged by the amount that you provision in GB per month until storage is released.
	
- Magnetic: charged by the number of requests to the volume
	
- Provisioned IOPS SSD: charged by the amount that you provision in IOPS (multiplied by the percentage of days that you provision for the month).



## Amazon Simple Storage Service (Amazon S3)

Amazon S3 is object-level storage, which means that if you want to change a part of a file, you must make the change and then re-upload the entire modified file. Amazon S3 stores data as objects within resources that are called **buckets**.


<h5>Amazon S3 overview</h5>

- Data is stored as objects in buckets
- Virtually unlimited storage
	- Single object is limited to 5 TB
- Designed for 11 9s of durability
- Granular access to bucket and objects

Amazon S3 is a manage cloud storage solution that is designed to scale seamlessly and provide 11 9s of durability. Bucket names are universal and must be unique across existing bucket names in Amazon S3.

The data that you store in Amazon S3 is not associated with any particular server, and you do not need manage any infrastructure yourself.

Objects can be almost any data file. You can even store database snapshots as objects. Amazon S3 also provides low-latency access to the data over the internet by HTTP or HTTPS, so you can retrieve data anytime from anywhere.

You can also encrypt your data, (not by default), in transit and choose to enable sever-side encryption on your projects.

### Amazon S3 storage classes

Amazon S3 offers a range of object-level storage classes that are designed for different use cases:

- **Amazon S3 Standard**: High durability, low latency, and high throughput storage for frequently accessed data. Best for apps, websites, gaming, content delivery, and analytics.
	
- **Amazon S3 Intelligent-Tiering**: Automatically moves data between frequent and infrequent access tiers based on usage. No retrieval fees, small monitoring cost. Ideal for unpredictable access patterns.
    
- **Amazon S3 Standard-IA**: Cheaper than Standard, for infrequently accessed but still important data. Fast retrieval when needed, used for backups and disaster recovery.
    
- **Amazon S3 One Zone-IA**: Stores data in only one Availability Zone, making it cheaper but less resilient. Good for secondary backups or re-creatable data.
	
- **Amazon S3 Glacier**: Archival storage with very low cost and retrieval times ranging from minutes to hours. Used for compliance and long-term data retention.
    
- **Amazon S3 Glacier Deep Archive**: The cheapest S3 option, for rarely accessed data (once or twice per year). Designed for long-term retention (7–10+ years), with 12-hour retrieval.




## Amazon Elastic File System (Amazon EFS)


## Amazon S3 Glacier



# Databases



# Cloud Architecture




# Auto Scaling and Monitoring




