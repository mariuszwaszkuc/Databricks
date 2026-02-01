# Data Engineering with Databricks Cookbook – Docker Environment (Modified)

This repository provides a modified and working Docker-based environment for running code examples from the book **_Data Engineering with Databricks Cookbook_** published by Packt.

## 📘 About This Repository

The original resources referenced in the book (such as Docker images and external links) were outdated or no longer available. This repository has been **updated and adapted** to ensure compatibility with current versions of Apache Spark, Delta Lake, and supporting tools.

### ✅ Key Modifications

- Updated `Dockerfile` and `docker-compose.yml` to use current and supported base images
- Replaced deprecated or broken URLs with working sources
- Verified compatibility with modern versions of Spark and related libraries
- Ensured successful build and execution using Docker Engine and Docker Compose

## ⚠️ Disclaimer

This repository **uses and adapts materials originally prepared by the authors of the book**, but it is **not an official release**. All modifications were made to restore functionality and improve usability for educational and practical purposes.


Ubuntu: Ubuntu 24.04.3 LTS
Docker: Docker version 28.5.0, build 887030f
Docker Compose: Docker Compose version v2.39.4
Python: Python 3.12.3
PIP: 
Git: git version 2.43.0

## 
Running the JupyterLab Environment with Apache Spark

1️⃣ Go to the Dockerfile directory

    cd ./docker/jupyterlab

    Make sure the directory contains the Dockerfile and any required files (e.g., .py or .ipynb notebooks).

2️⃣ Build the JupyterLab image
   
    docker build -t jupyterlab:4.2.5-spark-3.5.1 .
   
    -t → tags the image, making it easier to reference in docker-compose.
    . → build context (current directory).
    If the build fails, check the logs and make sure the Dockerfile has correct package versions and Spark paths.

3️⃣ (Optional) Test the image
    docker run -it --rm -p 8888:8888 jupyterlab:4.2.5-spark-3.5.1
    JupyterLab should start on port 8888 within a few seconds.
    Open in your browser: http://localhost:8888

4️⃣ Run the full environment with Docker Compose
    Go to the project root (where docker-compose.yml is located):
   
    cd ../../
   
    docker compose up --build
   
    --build → forces rebuilding all images (including JupyterLab).
    This will start:
    Spark Master
    Spark Workers
    Kafka + Zookeeper
    JupyterLab
    Kafka-UI


------------------------------------------------
# Data Engineering with Databricks Cookbook

<a href="https://www.packtpub.com/product/data-engineering-with-databricks-cookbook/9781837633357"><img src="https://content.packt.com/_/image/original/B19798/cover_image_large.jpg" alt="no-image" height="256px" align="right"></a>

This is the code repository for [Data Engineering with Databricks Cookbook](https://www.packtpub.com/product/data-engineering-with-databricks-cookbook/9781837633357), published by Packt.

**Build effective data and AI solutions using Apache Spark, Databricks, and Delta Lake**

## What is this book about?
This book shows you how to use Apache Spark, Delta Lake, and Databricks to build data pipelines, manage and transform data, optimize performance, and more. Additionally, you’ll implement DataOps and DevOps practices, and orchestrate data workflows.

This book covers the following exciting features:
* Perform data loading, ingestion, and processing with Apache Spark
* Discover data transformation techniques and custom user-defined functions (UDFs) in Apache Spark
* Manage and optimize Delta tables with Apache Spark and Delta Lake APIs
* Use Spark Structured Streaming for real-time data processing
* Optimize Apache Spark application and Delta table query performance
* Implement DataOps and DevOps practices on Databricks
* Orchestrate data pipelines with Delta Live Tables and Databricks Workflows
* Implement data governance policies with Unity Catalog

If you feel this book is for you, get your [copy](https://www.amazon.com/Engineering-Apache-Spark-Delta-Cookbook/dp/1837633355) today!

<a href="https://www.packtpub.com/?utm_source=github&utm_medium=banner&utm_campaign=GitHubBanner"><img src="https://raw.githubusercontent.com/PacktPublishing/GitHub/master/GitHub.png" 
alt="https://www.packtpub.com/" border="5" /></a>

## Instructions and Navigations
All of the code is organized into folders. For example, Chapter01.

The code will look like the following:
```
from pyspark.sql import SparkSession

spark = (SparkSession.builder
 .appName("read-csv-data")
 .master(«spark://spark-master:7077»)
 .config(«spark.executor.memory", "512m")
 .getOrCreate())

spark.sparkContext.setLogLevel("ERROR")
```

**Following is what you need for this book:**
This book is for data engineers, data scientists, and data practitioners who want to learn how to build efficient and scalable data pipelines using Apache Spark, Delta Lake, and Databricks. To get the most out of this book, you should have basic knowledge of data architecture, SQL, and Python programming.

With the following software and hardware list you can run all code files present in the book (Chapter 1-11).
### Software and Hardware List
| Chapter | Software required | OS required |
| -------- | ------------------------------------ | ----------------------------------- |
| 1-11 | Docker Engine version 18.02.0+ | Windows, Mac OS X, and Linux (any) |
| 1-11 | Docker Compose version 1.25.5+ | Windows, Mac OS X, and Linux (any) |
| 1-11 | Docker Desktop                 | Windows, Mac OS X, and Linux (any) |
| 1-11 | Git                            | Windows, Mac OS X, and Linux (any) |

### Related products
* Business Intelligence with Databricks SQL [[Packt]](https://www.packtpub.com/product/business-intelligence-with-databricks-sql/9781803235332) [[Amazon]](https://www.amazon.com/Business-Intelligence-Databricks-SQL-intelligence/dp/1803235330/ref=sr_1_1?crid=1QYCAOZP9E3NH&dib=eyJ2IjoiMSJ9.nKZ7dRFPdDZyRvWwKM_NiTSZyweCLZ8g9JdktemcYzaWNiGWg9PuoxY2yb2jogGyK8hgRliKebDQfdHu2rRnTZTWZbsWOJAN33k65RFkAgdFX-csS8HgTFfjZj-SFKLpp4FC6LHwQvWr9Nq6f5x6eg.jh99qre-Hl4OHA9rypXLmSGsQp4exBvaZ2xUOPDQ0mM&dib_tag=se&keywords=Business+Intelligence+with+Databricks+SQL&qid=1718173191&s=books&sprefix=business+intelligence+with+databricks+sql%2Cstripbooks-intl-ship%2C553&sr=1-1)

* Optimizing Databricks Workloads [[Packt]](https://www.packtpub.com/product/optimizing-databricks-workloads/9781801819077) [[Amazon]](https://www.amazon.com/Optimizing-Databricks-Workloads-performance-workloads/dp/1801819076/ref=tmm_pap_swatch_0?_encoding=UTF8&dib_tag=se&dib=eyJ2IjoiMSJ9.cskfrEglx5gEbJF-FnhxlA.rCtKm1bO6Fi1mXUpq1Oai0kjAhGseGT2cCZ2Ccgxaak&qid=1718173341&sr=1-1)

## Get to Know the Author
**Pulkit Chadha**
 is a seasoned technologist with over 15 years of experience in data engineering. His proficiency in crafting and refining data pipelines has been instrumental in driving success across diverse sectors such as healthcare, media and entertainment, hi-tech, and manufacturing. Pulkit’s tailored data engineering solutions are designed to address the unique challenges and aspirations of each enterprise he collaborates with.

