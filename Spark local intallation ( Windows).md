# DataOps_week_1
This repository contains all the code and documentation of the tasks that was given in Module 1 of L2 phase

# Soark Local Installation on Windows
There are some prerequisites before downloading Spark on our local system. These are :

### Instaling Java (SE Developement Kit):

[https://www.oracle.com/in/java/technologies/javase/javase8-archive-downloads.html](https://www.oracle.com/in/java/technologies/javase/javase8-archive-downloads.html)

Set the path variable :

To verify the installation: 
```
java -version
```

### Installing Scala (scala-2.13.11.msi) :

[https://www.scala-lang.org/download/2.13.11.html](https://www.scala-lang.org/download/2.13.11.html)

Set the path variable : 

To verify the installation: scala -verison

### Installing Apache Spark :

[https://spark.apache.org/downloads.html](https://spark.apache.org/downloads.html)

Select: 3.4.0 (Apr 13 2023)
Select: Pre-built for Apache Hadoop 3.3 and later (Scala 2.13)

To verify the downloaded file go to PowerShell and enter the belowe command: <br>
```
certutil -hashfile < path of the downloaded file > SHA 512
```

Match the output given by the above command and the SHA value available at :<br>[https://downloads.apache.org/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3-scala2.13.tgz.sha512](https://downloads.apache.org/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3-scala2.13.tgz.sha512)


### Now we need to extract the downloded file and set the required environment variables :

Step 1: For clean and organised installation
```
cd \
```
Step 2: 
```
mkdir spark 
```
**Now extract the downloaded file to this spark directory**
