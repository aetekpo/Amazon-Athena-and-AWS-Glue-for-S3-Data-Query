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
![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/Policy.png?raw=true)

We attached permissions policies such as AmazonS3FullAccess, AWSGlueServiceRole, AWSGlueConsoleFullAccess.

![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/Role.png?raw=true)

We created a role called GlueS3AccessRole and attached the policies to it.

## Step 3: Create an AWS Glue Crawler
A Glue Crawler scans your S3 bucket and automatically infers the schema, creating or updating tables in the Glue Data Catalog. We created a Crawler called Guardian_news_Crawler. Note that when creating your Crawler, select S3 as the data source and add (/) at the end of the data source path. e.g: s3://your-bucket-name/your-data-folder/.

![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/Crawler%20Success.png?raw=true)

Select the crawler created and run it. The crawler will scan the S3 bucket, infer the schema, and create/update tables in the Glue Data Catalog. After the crawler finishes, go to the table section in the Glue Console to verify if the table has been created and the schema matches your data.

![image_alt](https://github.com/aetekpo/Amazon-Athena-and-AWS-Glue-for-S3-Data-Query/blob/main/Table.png?raw=true)

## Step 4: Query Data Using Athena
We now need to query the data using Athena. If it’s the first time you are using Athena service, you need to set up query results location.
- Click on Manage and specify an S3 bucket to store query results. In this case, it will be s3://my-guardian-news-bucket/OutPut_Result/
- In the Athena query editor, select the Glue database created earlier or you can create a new database (guardian_news_db) and write a SQL query to query the table.
- SELECT * FROM guardian_news_db.guardian_news;
- Below is the result of the query we run.

![image_alt]()




