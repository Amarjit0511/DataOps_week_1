#### Array -> RDD using parallelize and also performing transformations.
```
import org.apache.spark.{SparkConf, SparkContext}

object rddd {
  def main(args: Array[String]): Unit = {
    // Create a SparkConf object
    val conf = new SparkConf().setAppName("rddd").setMaster("local[*]")

    // Create a SparkContext object
    val sc = new SparkContext(conf)

    // Create an RDD by parallelizing an existing collection
    val data = Array(1, 2, 3, 4, 5)
    val rdd = sc.parallelize(data)

    // Perform transformations and actions on the RDD
    val squaredRDD = rdd.map(x => x * x)
    val result = squaredRDD.collect()

    // Print the result
    result.foreach(println)

    // Stop the SparkContext
    sc.stop()
  }
}
```

#### csv -> RDD
```
import org.apache.spark.{SparkConf, SparkContext}
object csvRDD {
  def main(args: Array[String]): Unit={

    // Creating an object for Spark Configuration
    val conf=new SparkConf()
      .setAppName("csvRDD")
      .setMaster("local[*]")

    // Creating an object for SparkContext
    val sc =new SparkContext(conf)

    // Reading the file
    val rdd=sc.textFile("C:\\Datasets\\Supercharge_Locations.csv")

    // Printing the file
    val sample=rdd.take(10)
    sample.foreach(println)
  }

}
```

#### json -> RDD
```
import org.apache.spark.{SparkConf, SparkContext}
object jsonRDD {
  def main(args: Array[String]): Unit={

    //Creating a Configuration object for the application
    val conf=new SparkConf()
      .setAppName("jsonRDD")
      .setMaster("local[*]")

    //Creating a SparkContext object
    val sc=new SparkContext(conf)

    //Reading the data
    val rdd=sc.textFile("C:\\Datasets\\dwsample2-json.json")

    //Printing the sample data
    val sample=rdd.take(5)
    sample.foreach(println)

    sc.stop()
  }

}
```

#### parquet -> RDD
```
import org.apache.spark.{SparkConf, SparkContext}
object parquetRDD {
  def main(args: Array[String]): Unit={

    // Creating a configuration object for the application
    val conf=new SparkConf()
      .setAppName("parquetRDD")
      .setMaster("local[*]")

    //Creating a SparkContext object
    val sc=new SparkContext(conf)

    //Reading the data
    val rdd=sc.textFile("C:\\Datasets\\predictions.parquet")

    //Printing the sample data
    val sample=rdd.take(10)
    sample.foreach(println)

  }

}
```
