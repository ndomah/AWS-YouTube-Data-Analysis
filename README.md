# AWS YouTube Data Analysis
## Project Overview
- I will be working backwards, from “What does my customer need?”
- **The requirements from the (simulated) customer**:
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
- *Note: Ideally, it would be wise to use more recent data, but I couldn’t find any, and this dataset was very robust for the purposes of this project*
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
1. **Amazon S3 (Simple Storage Service)**: Amazon S3 is an object storage service known for its manufacturing scalability, data availability, security, and performance.
2. **AWS IAM (Identity and Access Management)**: AWS IAM is a critical component for managing access to AWS services and resources securely, ensuring proper authentication and authorization.
3. **Amazon QuickSight**: Amazon QuickSight is a scalable, serverless, machine learning-powered business intelligence (BI) service designed for the cloud. It facilitates data visualization and reporting.
4. **AWS Glue**: AWS Glue is a serverless data integration service that simplifies the process of discovering, preparing, and combining data for various purposes, including analytics, machine learning, and application development.
5. **AWS Lambda**: AWS Lambda is a serverless computing service that enables developers to run code without the need to manage servers. It's used for executing code in response to specific events.
6. **AWS Athena**: AWS Athena is an interactive query service designed for data stored in Amazon S3. It allows users to query data without the need to load it into a separate database; the data remains in S3, making it an efficient choice for querying large datasets.
These services are integral to the project and will collectively support data processing, storage, analysis, and reporting needs in an efficient and scalable manner.
## Workflow
1. **Data Ingestion**: Create an S3 Bucket for Raw Data. Upload YouTube data to the S3 bucket using the AWS CLI for efficient data partitioning and organization.
2. **Data Catalog and Initial Processing**: Utilize AWS Glue Data Catalog to establish a catalog for data. Implement a crawler to catalog both CSV and JSON files. The catalog output feeds into Amazon Athena, where tables within a database are created for data exploration.

![data catalog](https://github.com/ndomah/AWS-YouTube-Data-Analysis/blob/main/images/data%20catalog.jpeg)
3. **Data Pre-Processing**: Identify errors in the JSON format (SerDe) file structures. Develop an AWS Lambda function to preprocess and convert JSON files to Parquet format. Configure Lambda to trigger automatically upon data uploads to the S3 bucket. The processed data is stored in a separate S3 bucket and an associated Athena database, allowing schema and data type validation.

![pre-processing](https://github.com/ndomah/AWS-YouTube-Data-Analysis/blob/main/images/pre-processing.jpeg)
4. **ETL Processing for CSV Data**: Convert CSV files to Parquet format. Employ AWS Glue ETL job to further process and clean the data. Store the cleaned data in a designated S3 bucket.
5. **Additional Data Catalog and Database**: Create a second AWS Glue Data Catalog crawler to catalog the cleaned data. Populate a second database with cataloged tables.
6. **Data Integration and Final Preparation**: Build a new ETL job in AWS Glue to combine and join the cleaned tables. Store the integrated data in the final S3 bucket, ready for analytics.
7. **Analytics and Utilization**: The prepared data is now available for various applications, including dashboard reporting and machine learning models.
## QuickSight Dashboard
![dashboard](https://github.com/ndomah/AWS-YouTube-Data-Analysis/blob/main/images/dashboard.jpg)
## Key Questions Answered
The dashboard is designed to address the following key questions:
- **Which country had more views?** - The dashboard will display comparative views data for the USA, Great Britain, and Canada, allowing users to determine which country had the highest views.
- **Which video category had more views?** - The customer can explore the data to identify which video categories garnered the most views.
- **How did the views differ per category for the different regions?** - The dashboard provides a region-wise breakdown of views across different video categories, enabling the customer to understand variations in viewership.
