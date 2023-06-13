Say we have a csv file named ***Supercharge_Locations.csv*** at location ***"C:\Datasets\Supercharge_Locations.csv"***
### Converting the csv file to RDD:

```
val csvrdd=spark.read.csv(""C:\\Datasets\\Supercharge_Locations.csv")
```
***This RDD file will also have the first row as header names which if now removed will cause conflict with the data type when we create the schema***

### Removing the header row from the RDD:

***Getting the first row i.e. the header***
```
val header=csvrdd.first()
```

***Filtering out the header***
```
val withoutHeader=spark.filter(row=>row!=header)
```
### Creating the schema for the DataFrame

***Before we proceed with creating the schema, we need to import some libraries***
```
import org.apache.spark.sql._
import org.apache.spark.types._
import spark.implicits._
```

***Now we will be defining the schema***
```
val schema=StructType(Seq(
     |  StructField("Supercharger", StringType, nullable=true),
     |  StructField("Street Address", StringType, nullable=true),
     |  StructField("City", StringType, nullable=true),
     |  StructField("State", StringType, nullable=true),
     |  StructField("Zip", IntegerType, nullable=true),
     |  StructField("Country", StringType, nullable=true),
     |  StructField("Stalls", IntegerType, nullable=true),
     |  StructField("KW", DoubleType, nullable=true),
     |  StructField("GPS", DoubleType, nullable=true),
     |  StructField("Elev in m", IntegerType, nullable=true),
     |  StructField("GPS", DateType, nullable=true),
     |  StructField("Unknown", IntegerType, nullable=true)
     | ))
     
```
### Creating spark session
```
val session=SparkSession.builder().getOrCreate()
val sc=session.sparkContext
```

### Extracting the names of the columns from the schema and storing it as columnNames
```
val columnNames=schema.fields.map(_.name)
```

### Creating the DataFrame
```
val finalDataFrame=withoutHeader.toDF(columnNames: _*)
```

### To view the DataFrame
```
finalDataFrame.show()
```
