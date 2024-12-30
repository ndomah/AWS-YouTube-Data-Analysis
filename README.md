# AWS YouTube Data Analysis
## Project Overview
- I will be working backwards, from “What does my customer need?”
- The requirements from the (simulated) customer:
  - They are launching a new data-driven campaign
  - Their main advertising channel will be on YouTube
  - Initial questions to answer:
    - “How do we categorize videos based on their comments and statistics?”
    - “What factors affect how popular a YouTube video will be?”
## Why YouTube?
According to [https://explodingtopics.com/blog/most-visited-websites](https://explodingtopics.com/blog/most-visited-websites), in 2024 YouTube is the 2nd most visited website worldwide:
- Monthly Traffic:
  1. Google.com --> 132 billion
  2. YouTube.com --> 72 billion
  3. Facebook.com --> 12 billion
## The Dataset from YouTube
- Source: [https://www.kaggle.com/datasets/datasnaek/youtube-new](https://www.kaggle.com/datasets/datasnaek/youtube-new)
*Note: Ideally, it would be wise to use more recent data, but I couldn’t find any, and this dataset was very robust for the purposes of this project*
- It contains information on the top trending videos
- What does trending mean?
  - YouTube uses factors from user interactions to determine a Trending status
    - Number of views, shares, likes, and comments
    - It does NOT consider the most-viewed videos overall for the calendar year
- The Kaggle dataset collected the information directly using the YouTube API
## Project Goals:
1.	**Data Ingestion**: Build a mechanism to ingest data from different sources
2.	**ETL Design**: Since we are getting data in a raw format, we need to transform it into a workable format
3.	**Data Lake**: We will be getting the data from multiple sources, so we need a centralized repository to store them
4.	**Scalability**: As the size of our data increases, we need to make sure our system scales with it
5.	**Cloud**: We can’t process the vast amounts of data on our local computer, so we need to use the cloud (AWS)
6.	**Reporting**: Build a dashboard to get answers to the questions from the Project Overview
These goals collectively aim to establish a data pipeline that can efficiently handle, process, and analyze large datasets from diverse sources while ensuring scalability and ease of reporting through cloud-based infrastructure.
## Architecture
![architecture](https://github.com/ndomah/AWS-YouTube-Data-Analysis/blob/main/images/architecture.jpeg)
## Services Used
1. Amazon S3 (Simple Storage Service): Amazon S3 is an object storage service known for its manufacturing scalability, data availability, security, and performance.
2. AWS IAM (Identity and Access Management): AWS IAM is a critical component for managing access to AWS services and resources securely, ensuring proper authentication and authorization.
3. Amazon QuickSight: Amazon QuickSight is a scalable, serverless, machine learning-powered business intelligence (BI) service designed for the cloud. It facilitates data visualization and reporting.
4. AWS Glue: AWS Glue is a serverless data integration service that simplifies the process of discovering, preparing, and combining data for various purposes, including analytics, machine learning, and application development.
5. AWS Lambda: AWS Lambda is a serverless computing service that enables developers to run code without the need to manage servers. It's used for executing code in response to specific events.
6. AWS Athena: AWS Athena is an interactive query service designed for data stored in Amazon S3. It allows users to query data without the need to load it into a separate database; the data remains in S3, making it an efficient choice for querying large datasets.
These services are integral to our project and will collectively support data processing, storage, analysis, and reporting needs in an efficient and scalable manner.
## Workflow
1: Data Ingestion: 
  - Create an S3 Bucket for Raw Data. Upload YouTube data to the S3 bucket using the AWS CLI for efficient data partitioning and organization.
2: Data Catalog and Initial Processing:
Utilize AWS Glue Data Catalog to establish a catalog for data. Implement a crawler to catalog both CSV and JSON files. The catalog output feeds into Amazon Athena, where tables within a database are created for data exploration.

