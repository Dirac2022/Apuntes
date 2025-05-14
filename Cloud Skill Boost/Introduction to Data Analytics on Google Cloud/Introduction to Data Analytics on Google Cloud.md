Cuenta: daronmitchel
# Understand the Data Analytics Lifecycle on Google Cloud

## Understand the data analytics lifecycle on Google Cloud: Introduction

Capturing, managing, and using data is central to redefining customer experiences and creating new value.
The data analytics lifecycle provides a framework for organizing the different steps involved in data analytics.
Storing, managing and organizing your data is the foundation for data analytics on Google Cloud.

![[storing-managing-organizing.png]]

## Introducing a Google Cloud data analytics workflow
- Data comes from various different sources and inputs, including operational systems, web sources, social media, and internet of Things, or IoT.
- Data can also be structure or unstructured

![[structured-unstructured data.png]]



![[data analytics lifecycle.png]]


- Google Cloud provides serverless, comprehensive, and integrated solutions for each step of the data analytics lifecycle.
- The **data analytics lifecycle** is the process of collecting, storing, processing, and analyzing data to extract insights.
- The data analytics lifecycle is an iterative process. You will often go back and forth between different steps as you learn more about your data and what you want to achieve with it.

### Steps of the data analytics lifecycle
#### Ingest

![[ingest process tools.png]]

During this step, Google Cloud ingestion and processing tools help break down data silos and increase time to insight.
- **Pub/Sub**: Is a streaming analytics service for ingestion and messaging
- **Dataflow**: Is a streaming analytics service for analytics and processing.
- **Dataproc**
- **Cloud Data Fusion**: is a fully manage, cloud first, data integration service. This code-free, extract, transform, and load-or ETL -tool integrates data across on-premises and cloud sources.


>[!note] 
>- ETL: Extract (Data is gathered from various sources), Transform (Data is cleaned and formatted), Load (Data is stored in a target system, like a data warehouse).
>- on-premises: software or systems hosted on a company's physical servers, not in the cloud.

#### Process

After data is ingested, it needs to be processed.
1. **Dataproc** can be used to batch process data
2. **Dataflow** to stream data, or **Cloud Data Fusion** to integrate data from multiple sources.


#### Store
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

![[Storage Products.png]]


#### Analyze
After your data has been ingested, processed, and stored, it can be **analyzed**.

BigQuery is at the core of data analytics on Google Cloud.

>[!Important] BigQuery
>Is an elastic, flexible, secure, and reliable data warehouse that works across clouds and scales with your data. Can be used to analyze data though SQL commands.
>Is a serverless data warehouse for storage and analytics.

- BigQuery is deeply integrated with Google Cloud's analytical and data processing services.
- In addition to BigQuery, you can analyze data and visualize result by using **Looker** And **Looker Studio**.

![[ML products.png]]


Data is also the key to unlocking the value of Machine Learning on Google Cloud:
- Vertex AI: AutoML, Vertex AI Workbench and TensorFlow
These products unlock insights that only large amounts of data can provide.


## Google Cloud data sources and storage methods


Google Cloud offers several core storage products.
- Cloud Storage
- Cloud SQL
- Cloud Spanner
- BigQuery
- Firestore
- Cloud Bigtable
- AlloyDB (for PostgreSQL)

![[Store Products tools.png]]


### Data sources
Data sources are connectors that let you query data from various sources. You can use data sources to create datasets, which are collections of data that can be used for analysis and machine learning.

| Cloud data sources                          | External data sources                           |
| ------------------------------------------- | ----------------------------------------------- |
| Data sources that are stored on Gogle Cloud | Stored on-premises or in another cloud provider |
You can create a data sources connection by
- Google Cloud console
- Cloud SDK
- Google Cloud API

#### Benefits
- Centralize access to your data
- Integrate data from different sources (for building data warehouses and data lakes)
- Analyze your data (identify trends, make predictions, better business directions)
- Visualize your data

### Google Cloud storage options

![[Google cloud storage options.png]]


#### Database

##### Relational databases
- Cloud SQL
- Cloud Spanner
- AllowDB (for PostgreSQL)

##### Non-relational database
Is less structured in format and doesn´t use a tabular format. Non-relational databases follow a flexible data model, which makes them ideal for storing data that changes its organization frequently or for applications that handle diverse types of data. Example:
- BigTable


#### Data warehouse
Is designed to analyze data
A data warehouse is an enterprise system used for the analysis and reporting of structured and semi-structured data from multiple sources. Example:
- BigQuery

#### Data lake
A data lake is a repository designed to **ingest**, **store**, **explore**, **process**, and **analyze** any type or volume of raw data, regardless of the source.
It can store different types of data in its original form; ignoring size limits, and without much pre-processing or adding structure


>[!info] Altough Data warehouses and data lakes both store data in some capacity, each is optimized for different uses


### Types of data and uses

| Type              | Uses                                                                                           |
| ----------------- | ---------------------------------------------------------------------------------------------- |
| Structured data   | Is best fit for data analytics                                                                 |
| Unstructured data | Machine Learning algorithms can learn from this type to identify patterns and make predictions |

## Understand the data analytics lifecycle on Google Cloud: Summary

