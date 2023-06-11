# Spark DataFrames and DataSets and basic SQL operations

If we have a RDD we first need to convert it into a DataFrame with proper schema in place:



### Creating a DataFrame from a certain file format say CSV format:
```
val df=spark.read.format("csv").option("header", "true").load("path of the csv file")
df.createOrReplaceTempView("my_table")
```

#### Selcting all the records from the table
```
val result1=spark.sql("select * from my_table")
result1.show()
```

#### WHERE Clause
```
val result2=spark.sql("select * from my_table where _c4>10")
result2.show()
```

#### Sorting the table
```
val result3=spark.sql("select * from my_table order by _c4 asc")
result3.show()
```

#### Joining of two tables

Step 1: Loading the 2nd table
```
val df2=spark.read.format("csv").option("header", "true").load("path to the different csv file")
df2.createOrReplaceTempView("my_table_2")
```
Step 2: Joining both the table
```
val result4=spark.sql("select t1.____, t2.____ from my_table t1 join my_table_2 t2 on t1.id=t2.id")
result4.show()
```
