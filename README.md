# Big Data - "Alexa, can you handle big data?"


## Background

In this project, I will put my ETL skills to the test. Many of Amazon's shoppers depend on product reviews to make a purchase. Amazon makes these datasets publicly available. However, they are quite large and can exceed the capacity of local machines to handle. One dataset alone contains over 1.5 million rows; with over 40 datasets, this can be quite taxing on the average local computer. Your first goal for this assignment will be to perform the ETL process completely in the cloud and upload a DataFrame to an RDS instance. The second goal will be to use PySpark or SQL to perform a statistical analysis of selected data.


First I created DataFrames to match production-ready tables from two big Amazon customer review datasets.
Then analyzed whether reviews from Amazon's Vine program are trustworthy.

- - -

## Instructions

### Level 1

* Used the furnished schema to create tables in my RDS database.

* Created two separate Google Colab notebooks and **extract** any two datasets from the list at [review dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), one into each notebook.

  It is possible to ETL both data sources in a single notebook, but due to the large data sizes, it will be easier to work with these S3 data sources in two separate Colab notebooks.

  
* For each notebook (one dataset per notebook), complete the following:

  * Counted the number of records (rows) in the dataset.

  * **Transformed** the dataset to fit the tables in the [schema file](../Resources/schema.sql). Made sure the DataFrames match in data type and in column name.

  * **Loaded** the DataFrames that correspond to tables into an RDS instance. **Note:** This process can take up to 10 minutes for each. Again made sure that everything was correct before uploading.

### Level 2

In Amazon's Vine program, reviewers receive free products in exchange for reviews.

  ![vine01.png](../Images/vine01.png)

Amazon has several policies to reduce the bias of its Vine reviews: [https://www.amazon.com/gp/vine/help?ie=UTF8](https://www.amazon.com/gp/vine/help?ie=UTF8).

But are Vine reviews truly trustworthy? My task is to investigate whether Vine reviews are free of bias. By using either PySpark or SQL to analyze the data.


- - -

## Hints and Considerations

* I made sure to start each notebook with the following code in the first cell and update the Spark version.

```python
import os
# Find the latest version of spark 3.0  from http://www-us.apache.org/dist/spark/ and enter as the spark version
# For example:
# spark_version = 'spark-3.0.1'
spark_version = 'spark-3.<spark version>'
os.environ['SPARK_VERSION']=spark_version

# Install Spark and Java
!apt-get update
!apt-get install openjdk-11-jdk-headless -qq > /dev/null
!wget -q http://www-us.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop2.7.tgz
!tar xf $SPARK_VERSION-bin-hadoop2.7.tgz
!pip install -q findspark

# Set Environment Variables
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-11-openjdk-amd64"
os.environ["SPARK_HOME"] = f"/content/{spark_version}-bin-hadoop2.7"

# Start a SparkSession
import findspark
findspark.init()
```

* For connection to Postgres run the following code in the next cell.

```python
!wget https://jdbc.postgresql.org/download/postgresql-42.2.9.jar
```

- - -

Cleaned up all your AWS resources. Consulted the [AWS cleanup guide](../Resources/AWS_cleanup.pdf) and [AWS check billing guide](../Resources/AWS_check_billing.pdf) as reference.

* Downloaded my Google Colab notebooks as `.ipynb` files and uploaded those to GitHub.

* Copied my SQL queries into `.sql` files and uploaded them to GitHub.


## Rubric

[Unit 22 Rubric - Big Data Homework - "Alexa, can you handle big data?"](https://docs.google.com/document/d/1H-TBgBUz1jVGG1zvo046GraApmbepVZgYionh-4mNas/edit?usp=sharing)

- - -

## References

Amazon Customer Reviews Dataset. (n.d.). Retrieved April 08, 2021, from [https://s3.amazonaws.com/amazon-reviews-pds/readme.html](https://s3.amazonaws.com/amazon-reviews-pds/readme.html)

