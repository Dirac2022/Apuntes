
# AWS Concepts

**What is AWS?**

- Over 200 fully-featured services
- Global data centers
- Provides flexibility and scalability to support your goals


## Introduction to AWS

### Benefits of AWS

**Keys advantages of using the cloud**

- **Pay for what you use**
	- Consumption based model: start small and pay for what you use.
	- Allows for opportunities to save.
	
- **Economies of scale**: AWS has the ability to offer *pay-as-you-go* cost due to its vast customer base.
	
- **No more guessing capacity**: The ability to resize resources makes AWS elastic.
- **Increased speed and agility**
	- Rapid environment setup
	- Lower cost of failure
	
- **Save money on datacenters**: AWS manages infrastructure.
- **Go global in minutes**: Deploy applications to multiple regios quickly



### Introduction to the AWS Well-Architecture Framework

The Well-Architected Framework provides cloud architects with strategies and guidelines for
building resilient, scalable, and secure architectures on AWS

**The six pillars**
- **Security**
	- Protecting data, systems and assets.
	- Confidential data through robust identity and access management.
	- Controls to detect and mitigate security threats.
	
- **Cost Optimization**
	- Avoid unnecessary expenses.
	- Cost-effective decisions to ensure value on your cloud investment.
	
- **Performance Efficiency**
	- Compute resources used effectively.
	- Optimal performance to meet demands.
	- Efficiency as workloads evolve.
	
- **Sustainability**
	- Minimize environmental impact of running cloud.
	- Aligning your cloud strategy to your corporate environmental goals.
- **Operational Excellence**
	- Organize teams around business outcomes and implement observability for actionable insights.
	- Automate where possible.
	- Anticipate failure and learn from all operational events and metrics.
	- Use managed services
	
- **Reliability**
	- Automatically recover from failure.
	- Test recovery procedures.
	- Horizontal scaling


### Introduction to Cloud Migration

Moving your organizations data, applications, and workloads to the cloud.

**Benefits**
- Significant cost savings
- Increased flexibility
- Improved scalability

**AWS Cloud Adoption Framework (AWS CAF)**
Structured approach to help organizations design and implement a migration strategy

**The six perspectives**
- Business
- People
- Governance
- Platform
- Security
- Operations

<h5>Benefits of the Cloud Adoption Framework (CAF)</h5>
- **Reducing Risk**: ex. backing up data and defining transfer protocols.
- Optimize usage, reduce waste, lower energy consumption.
- **Increasing Revenue and Operational Efficiency**: Automate migration operations leading to greater operational efficiency.


<h5>Common migration strategies</h5>

**AWS Database Migration Service (DMS)**
Migrate databases and data in _real time_ or near real time from a source to a target.

- Replicating existing databases with minimal disruption
- Fully operational during transition

Typical use cases:
- Migrate an Oracle database to Amazon RDS.
- Replicate production data to the cloud with minimal downtime.
- Change database engines along with AWS Schema Conversion Tool (SCT).


**AWS Snowball**
Offline — you copy data locally onto the Snowball device, ship it back to AWS, and they load it into Amazon S3.

- Physical data transport for large-scale migrations
- For moving data quickly and securely

Typical use cases:
- Move tens or hundreds of terabytes when the network would be too slow or expensive.
- Transfer large media libraries, historical backups, or scientific datasets.


<h5>AWS Migration HUB</h5>

**AWS Migration Hub** is a service that helps you **plan, track, and manage application and data migrations** to AWS from a single place.

**Key points**

1. **Centralized tracking** – View the progress of all your migrations in a single dashboard, even if you use multiple AWS or partner tools.
    
2. **Discovery and planning** – Gather data on on-premises servers, usage, and dependencies to plan migration order and strategy.
    
3. **Tool integration** – Works with AWS migration tools (e.g., DMS, Application Migration Service) and selected partner solutions.

>[!info] In short
>AWS Migration Hub is like the **mission control** for your AWS migration journey — it won’t do the actual heavy lifting, but it keeps everything organized and visible in one place.


## Cloud Economics and Global Infrastructure



## The Core AWS Services