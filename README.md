# Home Sales Data Analysis with PySpark

![real-estate-and-big-data](https://github.com/dspataru/home-sales/assets/61765352/7fb25139-719a-4a3a-9ce2-bb768c212ee2)

## Table of Contents

## Introduction

Data analytics plays a crucial role in the real estate industry, including home sales. Data analytics allows real estate professionals to analyze market trends, comparable property prices, and economic indicators to set optimal listing prices. This helps sellers maximize their returns and ensures that homes are competitively priced. 

This repository contains a Jupyter Notebook, Home_Sales.ipynb, which performs data analysis on home sales data using PySpark. We use Spark to create temporary views, partition the data, cache and uncache a temporary table, and verify that the table has been uncached. Apache Spark is an open-source, distributed computing system that provides a fast and general-purpose cluster computing framework for big data processing, which is why it is favoured for this mini-project. V3.3.3 of Spark was used.

Google Colab was used to run the analysis. The following installations are required for this project:
1. !apt-get update
2. !apt-get install openjdk-11-jdk-headless -qq > /dev/null
3. !wget -q http://www.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop3.tgz
4. !tar xf $SPARK_VERSION-bin-hadoop3.tgz
5. !pip install -q findspark

#### Key Words
Apache Spark, PySpark, Jupyter Notebook, Google Colab, Partitions, Cache, Uncache, SQL queries, spark.sql, Parquet, home sales, data analytics, AWS, S3 bucket, dataframe

## Data Source

The data was taken from a csv file stored on AWS S3 bucket. A Spark session was created using the `SparkSession` library from pyspark. `SparkFiles` was used to extract information from the csv file and read the data into a dataframe. All of the data in the table is stored as a string. The data contains the following columns:
1. id: This is a unique ID for each of the homes stored in the database.
2. date: This column contains the date in YYYY-MM-DD format for when the listing was posted.
3. date_built: This column contains the year the house was built.
4. price: Price in $ of the home.
5. bedrooms: The number of bedrooms advertised.
6. bathrooms: The number of bathrooms advertised.
7. sqft_living: The size of the living space of the home in sqft.
8. sqft_lot: The size of the lot in sqft.
9. floors: The number of floors.
10. waterfront: This is a boolean value (0 or 1) where 0 represents no waterfront and 1 represents waterfront.

Below is a screenshot of the first 20 entries of the dataframe:

![home-sales-dataframe](https://github.com/dspataru/home-sales/assets/61765352/888fb85e-9aea-4aef-b171-60dc20fe0439)

## Data Analysis


