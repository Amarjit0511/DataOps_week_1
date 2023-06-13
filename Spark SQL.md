# Spark SQL

## Here in this demo we will be taking two DataFrames and perform various SQL queries on them

### Loading the first DataSet
```
val df=spark.read.format("csv").option("Header", "true").load("C:\\Datasets\\data.csv")
df.createOrReplaceTempView("my_table")
```

### Loading the second DataSet
```
val df2=spark.read.format("csv").option("Header", "true").load("C:\\Datasets\\Supercharge_Locations.csv")
df2.createOrReplaceTempView("my_table2")
```
