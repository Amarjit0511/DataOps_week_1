## Creating a temporary table for storing the persisted data : Example 1

```
import org.apache.spark.{SparkConf, SparkContext}
import org.apache.spark.storage.StorageLevel

object csvRDD {
    def main(args: Array[String]): Unit={
        
        // Creating a configuration object for the spark app
        val conf=new SparkConf()
          .setAppName("csvRDD")
          .setMaster("local[*]")
          
        // Creating an SparkContext 
        val sc=new SparkContext(conf)
        
        // Reading the data
        val df=sc.read.textFile("file location")
        
        // Persisting the data
        df.persist(STORAGELEVEL.MEMORY_ONLY)

        // Creating temporary table for persisted data
        df.createTempView("my_table")

        // Displaying the result
        val result = spark.sql("SELECT * FROM temp_table")
        result.show()

        // Unpersisting the data
        df.unpersist()

        // Stopping the spark session
        sc.stop()
    }
}
```

## Spark-shell implementation
```
imort org.apache.spark.sql.{Row, SparkSession}
import org.apache.spark.storage.StorageLevel
import org.apache.sql.types._
```
```
val spark=SparkSession.builder().appName("TempVariableForPersistedData").master("local[*]").getOrCreate()
```
```
val df=spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("C:\\Datasets\\industry_sic.csv")
```
```
df.persist(StorageLevel.MEMORY_ONLY)
```
```
df.createOrReplaceTempView("Temp_table_for_persisted_data")
```
```
val result=spark.sql("select * from "Temp_table_for_persisetd_data")
```
```
result.show()
```
![Screenshot 2023-06-16 014059](https://github.com/Amarjit0511/DataOps_week_1/assets/54772122/840ca939-1581-4daa-950b-07caf728fe9a)

### Note: To create the temporary view of the persisted data, the rdd first needs to be converted into DataFrame. 
### The rdd data created can be persisted, but to store that persisted data into temporary table, it first needs to be converted into DataFrame

