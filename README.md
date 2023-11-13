# Home Sales Data Analysis with PySpark

![real-estate-and-big-data](https://github.com/dspataru/home-sales/assets/61765352/7fb25139-719a-4a3a-9ce2-bb768c212ee2)

## Table of Contents
* [Introduction](https://github.com/dspataru/home-sales/blob/main/README.md#background)
* [Data Source](https://github.com/dspataru/home-sales/blob/main/README.md#data-source)
* [Data Analysis](https://github.com/dspataru/home-sales/blob/main/README.md#data-analysis)
* [Summary](https://github.com/dspataru/home-sales/blob/main/README.md#summary)


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

The following questions were answered using SparkSQL:
1. What is the average price for a four-bedroom house sold for each year? Round off your answer to two decimal places.

The query:
```sql
SELECT YEAR(date) AS year_sold, ROUND(AVG(price), 2) AS avg_price
FROM home_sales
WHERE bedrooms = 4
GROUP BY YEAR(date)
ORDER BY year_sold
```
The result:

![Q1-result](https://github.com/dspataru/home-sales/assets/61765352/e51f42dd-1b7b-440f-8481-38b0d2734cfc)


2. What is the average price of a home for each year it was built that has three bedrooms and three bathrooms? Round off your answer to two decimal places.

The query:
```sql
SELECT date_built AS year_built, ROUND(AVG(price), 2) AS avg_price
FROM home_sales
WHERE bedrooms = 3 AND bathrooms = 3
GROUP BY date_built
ORDER BY year_built
```

The result:

![Q2-result](https://github.com/dspataru/home-sales/assets/61765352/be939b60-e29d-403c-b196-71ecb82c24a4)


3. What is the average price of a home for each year that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet? Round off your answer to two decimal places.

The query:
```sql
SELECT date_built AS year_built, ROUND(AVG(price), 2) AS avg_price
FROM home_sales
WHERE bedrooms = 3 AND bathrooms = 3 AND floors = 2 AND sqft_living >= 2000
GROUP BY date_built
ORDER BY year_built
```

The result: 

![Q3-result](https://github.com/dspataru/home-sales/assets/61765352/5a87f13d-21a6-463b-94ac-333bda4d8c02)


4. What is the "view" rating for homes costing more than or equal to $350,000? Determine the run time for this query, and round off your answer to two decimal places.

The query:
```sql
SELECT view, ROUND(AVG(price), 2) AS avg_price
FROM home_sales
WHERE price >= 350000
GROUP BY view
ORDER BY view
```

## Summary

The result: 

![Q4-result](https://github.com/dspataru/home-sales/assets/61765352/e434d181-8d23-45c6-bdf1-169f3871d496)

