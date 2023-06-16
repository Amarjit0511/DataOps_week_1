## Launching Spark Shell

#### Go to the directory containing the extracte file 
```
spark-shell
```

## Importing necessary libraries

```
import org.apache.spark.sql.{DataFrame, SparkSession}
```
Spark Session: It provides an interface to interact with Spark. 
```
import org.apache.spark.sql.functions._
```
Enables data manipulation, transformation and analysis.

## Creating a spark session
```
val spark=SparkSession.builder().appName("Batch_Spark_Jobs").getOrCreate()
```
Creating a spark session will enable us to interact with spark and use various types of SQL operations on the Dataframes.

## Loading data of different formats
```
val csvData: DataFrame=spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("C:\\Datasets\\London_Airport.csv")
```
inferSchema when set to true enables spark to automatically guess the structure of the data.
Setting inferSchema to true can be an expensive process when dealing with large datasets and hence explicity defining the schema is preferred.
```
val jsonData: DataFrame=spark.read.format("json").option("inferSchema", "true").load("C:\\Datasets\\tweets.json")
```
```
val parquetData=spark.read.format("parquet").option("inferSchema", "true").load("C:\\Datasets\\val.parquet")
```

## Creating temporary table for the data
```
csvData.createOrReplaceTempView("csvTable")
```
Creates a temporary table for performing Spark SQL queries.
```
jsonData.createOrReplaceTempView("jsonTable")
```
```
parquetData.createOrReplaceTempView("parquetTable")
```

## Performing an SQL Query
```
val result: DataFrame = spark.sql(""" select * from csvTable where `number_of_reviews`>10""")
```

## Persisting data as csv
```
result.write.mode("append").option("header", "true").csv("C:\\Datasets\\persisted_data\\csv_persisted")
```
Stores the data in memory or disk as per the choice of the user for immediate use.

## Persisting data as json
```
result.write.mode("append").option("header", "true").json("C:\\Datasets\\persisted_data\\json_persisted")
```

## Persisting data as parquet
```
result.write.mode("append").option("header", "true").parquet("C:\\Datasets\\persisted_data\\parquet_persisted")
```

## Repartioning the data
```
val repartitionedData: DataFrame = result.repartition(col("number_of_reviews"))
```
Repartitioning is done to partition the data across partitions of a DataFrame.
We can use the col function here only because we imported the functions library from the apache spark sql library.
It can involve data shuffling to ensure that data with common attributes are put in the same partition, but this can lead to network ovehead.

![Screenshot 2023-06-16 064903](https://github.com/Amarjit0511/DataOps_week_1/assets/54772122/acaae0f2-0044-40ee-8cc1-1556afa378e9)

## Coalesced Data
```
val coalescedData: DataFrame = result.coalesce(2)
```
It decreases the number of partitions by combining adjaent partitions into larger partitions. 
It is used to remove the overhead of managing many different partitions by clubbing them.

![Screenshot 2023-06-16 065017](https://github.com/Amarjit0511/DataOps_week_1/assets/54772122/67a324b3-e37d-4b64-a3aa-d92ee2f012e0)
