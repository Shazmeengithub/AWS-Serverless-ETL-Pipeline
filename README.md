# Project Title: AWS Serverless ETL Pipeline | Event-Driven Data Lake Automation ☁️

Building a fully automated, **event-driven serverless ETL pipeline** on AWS to process JSON data into Parquet format and make it queryable through Amazon Athena — without any manual scheduling or servers.

---

## Table of Contents
- <a href="#overview">Overview</a>
- <a href="#architecture">Architecture</a>
- <a href="#aws-services">AWS Services Used</a>
- <a href="#tools">Tools & Technologies</a>
- <a href="#data-flow">Data Flow</a>
- <a href="#key-concepts">Key Concepts Demonstrated</a>
- <a href="#cost">Cost and Scalability</a>
- <a href="#how-to-run">How to Run the Project?</a>

---

<h2 id="overview">Overview</h2>

This project demonstrates how to build a **fully automated ETL (Extract, Transform, Load) pipeline** using AWS serverless services.  
Whenever a JSON file is uploaded to an S3 bucket, a **Lambda function** automatically processes and transforms it into **Parquet format**, stores it in a data lake, updates the **Glue Data Catalog**, and enables instant querying through **Amazon Athena**.

---

<h2 id="architecture">Architecture</h2>

**Workflow:**
1. A JSON file is uploaded to an **S3 bucket**.
2. The **S3 event** triggers an **AWS Lambda** function.
3. Lambda reads and flattens the JSON data using **Python (Pandas)**.
4. The transformed data is converted into **Parquet format** and stored back in S3.
5. Lambda triggers an **AWS Glue Crawler** to update the schema in the **Glue Data Catalog**.
6. The data becomes queryable using **Amazon Athena** via SQL.

**End-to-End Flow:**  
`S3 (Raw JSON) ➜ Lambda ➜ S3 (Parquet Data Lake) ➜ Glue Crawler ➜ Glue Catalog ➜ Athena`
<img width="1269" height="196" alt="image" src="https://github.com/user-attachments/assets/4db9863f-7985-4dd6-8221-bc8d3e7b5610" />

---

<h2 id="aws-services">AWS Services Used</h2>

| Service | Purpose |
|----------|----------|
| **Amazon S3** | Storage for raw JSON and transformed Parquet files |
| **AWS Lambda** | Serverless compute for transformation logic |
| **AWS Glue Crawler** | Automatically updates schema and catalog |
| **AWS Glue Data Catalog** | Stores metadata about the data lake |
| **Amazon Athena** | SQL querying directly on S3 data |

---

<h2 id="tools">Tools & Technologies</h2>

* **Programming:** Python 3.x  
* **Libraries:** Pandas, Boto3, PyArrow  
* **AWS Services:** S3, Lambda, Glue, Athena  
* **Architecture Type:** Serverless, Event-Driven  
* **File Formats:** JSON → Parquet  

---

<h2 id="data-flow">Data Flow</h2>

1. Upload `orders_ETL.json` to S3 (`orders_json_incoming/` folder).
2. **Lambda Triggered:** Reads JSON → Flattens → Converts to Parquet.
3. **Saves to:** `orders_parquet_datalake/` folder in S3.
4. **Glue Crawler:** Updates table schema in the Glue Catalog.
5. **Athena:** Queries data instantly using SQL.

---

<h2 id="key-concepts">Key Concepts Demonstrated</h2>

- **Event-driven ETL pipeline** with automatic triggers  
- **Serverless data transformation** using AWS Lambda  
- **Schema discovery and metadata** via AWS Glue  
- **Data lake architecture** using Amazon S3 + Parquet  
- **SQL analytics** on data lakes via Amazon Athena  
- **Fully automated** with no manual scheduling or server provisioning  

---

<h2 id="cost">Cost and Scalability</h2>

- **AWS Free Tier compatible** — minimal to zero cost for demo.  
- **Pay-as-you-go model** for Lambda and Athena.  
- **Serverless auto-scaling** — dynamically adjusts to workload.  
- Suitable for **small to enterprise-scale** data ingestion.  

---

<h2 id="how-to-run">How to Run the Project?</h2>

1. **Create an AWS Account** (Free Tier works).  

2. **Create S3 Buckets:**
   - `orders_json_incoming/` → for raw JSON data  
   - `orders_parquet_datalake/` → for processed data  

3. **Set up AWS Lambda:**
   - Runtime: **Python 3.x**  
   - Add **S3 Trigger** → `orders_json_incoming/` folder  
   - **IAM Role Permissions:**
     - `AmazonS3FullAccess`  
     - `AWSGlueServiceRole`   
   - Add **AWS SDK Pandas Layer** for `pandas` + `pyarrow` support  

4. **Deploy Lambda Code:**
   - Upload your `lambda_function.py` and helper flatten function to Lambda.  

5. **Create AWS Glue Crawler:**
   - **Source:** S3 path → `orders_parquet_datalake/`  
   - **Target:** New Glue Database (e.g., `etl_pipeline_db`)  

6. **Run the Process:**
   - Upload JSON → Lambda Trigger → Parquet → Crawler → Athena Query  

7. **Query via Athena:**
   - Select the Glue table → Run SQL queries instantly.  

---
