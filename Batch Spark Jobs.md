## Launching Spark Shell

#### Go to the directory containing the extracte file 
```
spark-shell
```

## Importing necessary libraries

```
import org.apache.spark.sql.{DataFrame, SparkSession}
```
```
import org.apache.spark.sql.functions._
```

## Creating a spark session
```
val spark=SparkSession.builder().appName("Batch_Spark_Jobs").getOrCreate()
```

## Loading data of different formats
```
val csvData: DataFrame=spark.read.format("csv").option("header", "true").option("inferSchema").load("C:\\Datasets\\London_Airport.csv")
```
```
val jsonData: DataFrame=spark.read.format("csv").option("inferSchema", "true").load("C:\\Datasets\\tweets.json")
```
```
val parquetData=spark.read.format("parquet").option("inferSchema", "true").load("C:\\Datasets\\val.parquet")
```

## Creating temporary table for the data
```
csvData.createOrReplaceTempView("csvTable")
```
```
jsonData.createOReplaceTempView("jsonTable")
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
result.write.mode("overwrite").option("header", "true").csv("C:\\Datasets\\persisted_data\\csv_persisted")
```

## Persisting data as json
```
result.write.mode("overwrite").option("header", "true").json("C:\\Datasets\\persisted_data\\json_persisted")
```

## Persisting data as parquet
```
result.write.mode("overwrite").option("header", "true").parquet("C:\\Datasets\\persisted_data\\parquet_persisted")
```

