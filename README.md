# ppepiline_aws
🚀 End-to-End Data Engineering Pipeline: From Ingestion to Data Lakehouse
This project consists of a complete Data Engineering pipeline developed in Python to automate public data extraction, transform formats for storage optimization (Parquet), and catalogue the data using AWS Glue.

The goal is to build a scalable Data Lake architecture on AWS, moving data from a raw state (Bronze) to a structured and queryable state (Silver initialization) using Serverless technologies.

🛠️ Architecture & Workflow
The data flow follows these steps:

Extraction (ELT): Automated collection of raw CSV files (Boston 311 Service Requests) directly from the open data portal.

Transformation:

Consolidation of data using Pandas.

Conversion from CSV to Parquet (columnar format) for storage efficiency and query performance.

Storage (Bronze Layer): Uploading the Parquet files to Amazon S3, organized by year in the bronze/ directory.

Cataloging (Silver Layer Enablement):

Triggering an AWS Glue Crawler to scan the S3 bucket.

Automatic schema inference and metadata storage in the AWS Glue Data Catalog.

This makes the data immediately queryable via Amazon Athena.

🧰 Tech Stack
Language: Python 3.12

ETL & Manipulation: Pandas, PyArrow

AWS SDK: Boto3

Cloud Storage: Amazon S3 (Simple Storage Service)

Data Governance & Catalog: AWS Glue (Crawler & Data Catalog)

Query Engine: Amazon Athena (Serverless SQL)

📋 Implementation Details
1. Ingestion & Optimization (Python + S3)
The pipeline uses requests to download datasets (2015-2020) and processes them in-memory using BytesIO. The data is converted to Parquet before being uploaded to S3. This reduces storage costs and improves I/O speed compared to raw CSVs.

2. Automating the Silver Layer (AWS Glue Crawler)
To move beyond simple file storage, I implemented an AWS Glue Crawler.

Schema Discovery: The Crawler automatically detects the schema (column names, data types) of the Parquet files stored in the Bronze layer.

Metadata Management: It populates the AWS Glue Data Catalog, creating a centralized repository of metadata.

Handling Schema Evolution: If new columns are added to the source data in the future, the Crawler is configured to update the table definition automatically.
