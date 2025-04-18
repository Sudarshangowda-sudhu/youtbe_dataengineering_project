# youtbe_dataengineering_project
YouTube Data Engineering Project on AWS
This project demonstrates a complete data engineering pipeline built on AWS to ingest, transform, analyze, and visualize trending YouTube video data from multiple countries.

Project Overview

The main goal of this project is to securely manage, optimize, and analyze structured and semi-structured data from YouTube's trending video dataset. The pipeline supports scalable, cloud-based processing with a final dashboard for insights.

Project Goals

Ingestion: Ingest data from different formats (CSV and JSON) and locations.

Data Lake: Store raw and clean data in a centralized, scalable Amazon S3 bucket.

ETL System: Clean, transform, and enrich raw data for analysis.

Cloud-first: Leverage AWS for scalable, serverless processing.

Reporting: Build a dashboard with Amazon Quicksight for business users and analysts.

AWS Services Used

Amazon S3: Centralized storage for raw and processed data.

AWS IAM: Secure access to AWS resources.

AWS Glue: Serverless data integration, schema detection, and ETL pipelines.

AWS Lambda: Serverless compute for processing semi-structured JSON files.

Amazon Athena: SQL-based querying of S3 data.

Amazon Quicksight: BI and data visualization layer.

Dataset Dataset: "Trending YouTube Video Statistics" from Kaggle
Link: https://www.kaggle.com/datasets/datasnaek/youtube-new
Format: CSV for trending stats per region, JSON for category metadata.

Architecture and Workflow

Data Ingestion

Upload CSV (per region) and JSON (metadata) files to S3 using AWS CLI.

Organize data into appropriate folders: raw_statistics and raw_statistics_reference_data.

Schema Detection

Use AWS Glue Crawlers to infer schemas and create tables in the Glue Data Catalog.

Data Cleaning and Transformation

AWS Lambda: Normalize JSON arrays using awswrangler and convert to Parquet.

AWS Glue ETL Jobs: Clean and transform CSV data using Visual ETL interface.

Partition data by region or category for efficient querying.

Querying with Athena

Query both JSON and CSV tables.

Join tables like raw_statistics and cleaned_statistics_reference_data.

Store Athena query outputs in a dedicated S3 output bucket.

Data Modeling

Use AWS Glue ETL to join and enrich data, producing a final analysis-ready dataset.

Final table partitioned by category_id and stored in a new bucket.

Visualization with Quicksight

Import final Athena table into Quicksight.

Build interactive dashboards and visuals to answer analytical questions.

Sample Athena Query

SELECT a.title, a.category_id, b.snippet_title
FROM de_youtube_raw.raw_statistics a
INNER JOIN de_youtube_raw.cleaned_statistics_reference_data b
ON a.category_id = CAST(b.id AS INT)
WHERE region = 'us';

Future Improvements

Automate Lambda trigger on file upload

Schedule Glue ETL jobs

Add time-series forecasting or anomaly detection using Quicksight
