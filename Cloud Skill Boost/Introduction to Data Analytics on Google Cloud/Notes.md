
# Understand the Data Analytics Lifecycle on Google Cloud

Storing, managing and organizing your data is the foundation for data analytics on Google Cloud.

![[data analytics lifecycle.png]]


- Google Cloud provides serverless, comprehensive, and integrated solutions for each step of the data analytics lifecycle.
- The **data analytics lifecycle** is the process of collecting, storing, processing, and analyzing data to extract insights.
- The data analytics lifecycle is an iterative process
- You will often go back and forth between different steps as you learn more about your data and what you want to achieve with it.

## Steps of the data analytics lifecycle
### Ingest data into the cloud
During this step, Google Cloud ingestion and processing tools help break down data silos and increase time to insight.
- **Pub/Sub**: Is a streaming analytics service for ingestion and messaging
- **Dataflow**: Is a streaming analytics service for analytics and processing.
- **Dataproc**
- **Cloud Data Fusion**: is a fully manage, cloud first, data integration service. This code-free, extract, transform, and load-or ETL -tool integrates data across on-premises and cloud sources.


>[!note] 
>- ETL: Extract (Data is gathered from various sources), Transform (Data is cleaned and formatted), Load (Data is stored in a target system, like a data warehouse).
>- on-premises: software or systems hosted on a company's physical servers, not in the cloud.


After data is ingested, it needs to be processed.
1. Dataproc can be used to batch process data
2. Dataflow to stream data, or Cloud Data Fusion to integrate data from multiple sources.

One data has been ingested and processed, the next step is to store the data securely: databases, data lakes, data warehouses. Google storage products:

- Relational databases:
	- Cloud SQL
	- Cloud Spanner
	- AlloyDB (for PostgreSQL)
- NoSQL databases:
	- Bigtable
	- Firestore
- Cloud Storage
- BigQuery: data warehouse solution.

After your data has been ingested, processed, and stored, it can be **analyzed**.

>[!Important] BigQuery
>Is an elastic, flexible, secure, and reliable data warehouse that works across clouds and scales with your data. Can be used to analyze data though SQL commands.

Google Cloud offers several core storage products.
- Cloud Storage
- Cloud SQL
- Cloud Spanner
- BigQuery
- Firestore
- Cloud Bigtable
- AlloyDB (for PostgreSQL)

![[Storage Products.png]]