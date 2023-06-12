# Word Count 

### Reading data in RDD
```
val data=spark.read.option("header", "true").csv("C:\Datasets\industry_sic.csv")
```

### Now select the column which contains the string
```
val textColumn=data.select("Description")
```
### Splitting the string into individual words
```
import org.apache.spark.sql.function._
val words=textColumn.select(explode(split(col("Description"), " ")).alias("word"))
```

### Performing word count
```
val wordCount=words.groupBy("word").count()
```
### To view the output
```
wordCount.show()
```
