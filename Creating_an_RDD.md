## Different ways to ceate an RDD in Spakr (3 Different Ways):

### 1: Using Paralllize:
A sequence, a list, or an array, etc can be converetd to an array by the paralleilise method:
```spark
val rdd1=spark.sparkContext.parallelize(Array[String]("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"))
```
or 
```
val rdd1=spark.sparkContext.parallelize(Seq("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"))
```
We can also specify the partition size on our own:

``` spark 
val rdd1=spark.sparkContext.parallelize(Array("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"),2)
```
***To get a default view of the partitoned Array:***
```
rdd1.glom().foreach(println)
```

***To get a understandable view of the partitioned data***
```
rdd1.foreach(println)
```

### 2. Using External Dataset:
#### To convert textfile into RDD:
```val rddtext=spark.read.textFile("path to the text file")```

***Some of the operation that we can perform to confirm the RDD creation are***
1. collect()
2. count()
3. take(n)
4. foreach(func)

***To display the content of the RDD***
```
val content = rddtext.collect()
println("The content of the RDD is" +content)
```

***To display the sample of the content say first 20 elements***
```
val sampleContent=rddtext.take(20)
sampleContent.foreach(println)
```

***To check the number of elements in RDD:***
```
val count=rddtext.count()
println("The number of elements in the RDD is" +rddtext)
```

#### To convert csv into RDD:
```
val rddcsv=spakr.read
           .csv(" path to csv file ")
           .rdd
```

***To display the sample content***
```
val csvSample=rddcsv.take(20)
csvSample.foreach(println)
```

#### To convert json into RDD:
```
val rddjson=spark.read
            .json(" path to json file ")
            .rdd
 ```
 
 ***To display the sample content***
 ```
 val jsonSample=rddjson.take(20)
 jsonSample.foreach(println)
 ```
 
 #### To convert parquet file into RDD:
 ``` 
 val rddparquet=spark.read
             .parquet(" path to parquet file ")
             .rdd
 ```
 
 ***To view the sample file***
 ```
 val parquetSample=rddparquet.take(20)
 parquetSample.foreach(println)
```

### 3. Using an exiting RDD
```
val oldRDD=spark.read.TextFile(" path to the existing textfile RDD ")
val split=oldRDD.flatMap(line => line.split(" "));
val mapdata=split.map(word => (word,1));
mapdata.collect
```

## Converting an RDD back to DataFrame or DataSet

RDD created does not have any schema, hence when converting it into DataFrame or DataSet it is necessary for us to define the schema as well and then map the values into the schema.

Suppose we create a text RDD:
```
val rddtext = spark.sparkContext.textFile(" path of the text file ")
```

***Define the schema for the DataFrame***

First we will have to import necessary libraries
```
import org.apache.spark.sql.Row
import org.apache.spark.sql.types._
```
```
val schema = StructType(Seq(StructField("Line", StringType, nullable = True)))
```

***The above schema has only one column with the datatype of String also nullable = True means that the column can have null values as well***

Now after the RDD is there in place and we also have a schema where we can map the data in RDD, we have to map the value in RDD to the schema to create a DataFrame

```
val df= spark.createDataFrame(rddtext.map(Row(_)), schema)
df.show()
```

## Converting a csvrdd back to DataFrame

```
val csvrdd=spark.read.csv("path to csv file").rdd
```

#### Note: If the csv file had headers as well, it becomes necessary to remove the header else it will cause conflict with the schema of the DataFrame

```
val header=csvrdd.first()
```

```
val withoutHeader=csvrdd.filter(row => row!=header)
```
We can view the transformed rdd by:
```
val sample=withoutHeader.take(10)
sample.foreach(println)
```

Now that the csvrdd file is created now we will create a schema for it to be mapped back into DataFrame

```
import org.apache.spark.sql.Row
import org.apache.spark.sql.types._
val schema=StryctType(Seq(
    StructField("Col_1_name", DoubleType, nullable=true),
    StrcutField("Col_2_name", DoubleType, nullable=true),
    StructField("Col_3_name", DoubleType, nullable=true),
    StructField("Col_4_name", DoubleType, nullable=true)
    ))
```

Now that we have a schema in place, we will map the csvrdd to this schema:
```
val df=spark.createDataFrame(csvrdd.map(Row(_)), schema)
df.show()
```

