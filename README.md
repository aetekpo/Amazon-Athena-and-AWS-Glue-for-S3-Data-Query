# Amazon-Athena-and-AWS-Glue-for-S3-Data-Query
## Overview
In this blog, we will explain how to query data stored in an S3 bucket using AWS Athena, Glue Crawler, and AWS Glue Data Catalog. This lab demonstrates steps to follow:
## Architecture Diagram
![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/Glue%20Image.png?raw=true)

## What is Amazon Athena?

AWS Athena is a serverless interactive query service provided by Amazon Web Services (AWS). It allows you to analyze large datasets stored in Amazon S3 using SQL queries. It supports querying structured, semi-structured, and unstructured data like JSON, CSV, Parquet, and ORC.

## Step 1: Set up the S3 Bucket

Ensure the data you want to query is stored in an S3 bucket in a structured format (e.g., CSV, JSON, Parquet, etc.).
If the data is not stored, then create an S3 bucket and upload the data.
The data in the S3 bucket is the source data.
Create a destination output S3 bucket. This can be another S3 bucket or you can create a folder under the first S3 bucket. In this project, we will create a folder called Output Result where we will store the queried data.
![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/S3_Image.png?raw=true)

## Step 2: Configure IAM Role

IAM stands for Identity and Access Management. It is a web service that helps you securely control access to AWS resources. With IAM, you can manage who (identity) can access what (resources) and under what conditions.
We created a custom policy called GlueS3AccessPolicy. We used this JSON editor to define the policy. This minimizes security risks by ensuring that Glue only has access to the resources it needs. Make sure to replace “your-bucket-name” with the name of your S3 bucket.

