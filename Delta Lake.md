### Delta lake format is nothing but Apache Parquet files with transaction log. It has got multiple pipelne for reading and writing data concurrently.

### Why do we use Delta Lake?
#### ACID Transactions on Data Lakes
#### Schema Enforcement

## Creating a Delta Lake

### Reading the data
```
val people = spark.read.load("/databricks-datasets/learning-spark-v2/people/people-10m.delta")
people.show()
```

### Writing data to table
```
people.write.saveAsTable("people_10m")
```

### To get the location of the table
```scala
display(spark.sql("DESCRIBE DETAIL people_10m"))

```

### We can also create a new empty Delta table that duplicates the schema and table properties for a source Delta table.
```
// Create table in the metastore
DeltaTable.createOrReplace(spark)
  .tableName("default.people10m")
  .addColumn("id", "INT")
  .addColumn("firstName", "STRING")
  .addColumn("middleName", "STRING")
  .addColumn(
    DeltaTable.columnBuilder("lastName")
      .dataType("STRING")
      .comment("surname")
      .build())
  .addColumn("lastName", "STRING", comment = "surname")
  .addColumn("gender", "STRING")
  .addColumn("birthDate", "TIMESTAMP")
  .addColumn("ssn", "STRING")
  .addColumn("salary", "INT")
  .execute()

// Create or replace table with path and add properties
DeltaTable.createOrReplace(spark)
  .addColumn("id", "INT")
  .addColumn("firstName", "STRING")
  .addColumn("middleName", "STRING")
  .addColumn(
    DeltaTable.columnBuilder("lastName")
      .dataType("STRING")
      .comment("surname")
      .build())
  .addColumn("lastName", "STRING", comment = "surname")
  .addColumn("gender", "STRING")
  .addColumn("birthDate", "TIMESTAMP")
  .addColumn("ssn", "STRING")
  .addColumn("salary", "INT")
  .property("description", "table with people data")
  .location("/tmp/delta/people10m")
  .execute()
```

### Upsert to a table
```sql
CREATE OR REPLACE TEMP VIEW people_updates (
  id, firstName, middleName, lastName, gender, birthDate, ssn, salary
) AS VALUES
  (9999998, 'Billy', 'Tommie', 'Luppitt', 'M', '1992-09-17T04:00:00.000+0000', '953-38-9452', 55250),
  (9999999, 'Elias', 'Cyril', 'Leadbetter', 'M', '1984-05-22T04:00:00.000+0000', '906-51-2137', 48500),
  (10000000, 'Joshua', 'Chas', 'Broggio', 'M', '1968-07-22T04:00:00.000+0000', '988-61-6247', 90000),
  (20000001, 'John', '', 'Doe', 'M', '1978-01-14T04:00:00.000+000', '345-67-8901', 55500),
  (20000002, 'Mary', '', 'Smith', 'F', '1982-10-29T01:00:00.000+000', '456-78-9012', 98250),
  (20000003, 'Jane', '', 'Doe', 'F', '1981-06-25T04:00:00.000+000', '567-89-0123', 89900);

MERGE INTO people_10m
USING people_updates
ON people_10m.id = people_updates.id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *;
```
### Querying the table for results
``` sql
selct * from people_10 where id>=9999998
```

### Reading the table
```
val people_df=spark.read.table(table_name)
display(people_df)
```

### Writing to a table


