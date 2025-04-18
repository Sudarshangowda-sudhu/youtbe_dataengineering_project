# youtbe_dataengineering_project
YouTube Data Engineering Project on AWS

This project demonstrates a complete data engineering pipeline built on AWS to ingest, transform, analyze, and visualize trending YouTube video data from multiple countries.

Project Overview

The main goal of this project is to:

Securely manage structured and semi-structured data

Optimize data processing in a scalable way

Analyze data using serverless tools

Deliver insights through visualizations

Project Goals

Ingestion: Ingest data from multiple formats (CSV and JSON)

Data Lake: Store all data in a centralized S3 bucket

ETL System: Clean, transform, and structure raw data

Cloud-first: Use AWS to scale and automate

Reporting: Create a Quicksight dashboard for visualization

AWS Services Used

Amazon S3: Store raw and clean data

AWS IAM: Manage secure access to AWS resources

AWS Glue: Discover schema and run ETL jobs

AWS Lambda: Process and clean JSON data

Amazon Athena: Query S3 data with SQL

Amazon Quicksight: Create interactive dashboards

Dataset

Source: Kaggle - Trending YouTube Video Statistics
(https://www.kaggle.com/datasets/datasnaek/youtube-new)

Format:

CSV for regional trending video stats

JSON for category metadata

Architecture & Workflow

Data Ingestion

Upload CSV and JSON files to S3 using AWS CLI

Organize data in folders:

raw_statistics/

raw_statistics_reference_data/

Schema Detection

Use Glue Crawlers to infer schemas and create tables in the Data Catalog

Data Cleaning & Transformation

Use AWS Lambda to:

Normalize JSON arrays (like items)

Convert to Parquet

Use AWS Glue Visual ETL to:

Clean CSV data

Change data types

Store clean data in another S3 bucket

Partition data by region or category_id

Querying with Athena

Run SQL queries on cleaned data

Join JSON and CSV tables

Store Athena results in a separate output bucket

Data Modeling

Use AWS Glue ETL to:

Join raw and reference tables

Create final analysis-ready tables

Partition tables for performance

Visualization

Import final Athena table into Quicksight

Create dashboards and charts for insights

Sample Athena Query

Join trending videos with category metadata:

SELECT a.title, a.category_id, b.snippet_title
FROM de_youtube_raw.raw_statistics a
INNER JOIN de_youtube_raw.cleaned_statistics_reference_data b
ON a.category_id = CAST(b.id AS INT)
WHERE region = 'us';
Schedule Glue ETL jobs

Add time-series forecasting or anomaly detection using Quicksight
