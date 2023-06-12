# Downloading Spark locally on MAC Operating System

Before downloading Spark there are some pre-requisites that we need for Spark to work:

### Downloading Java:
[https://www.oracle.com/in/java/technologies/downloads/](https://www.oracle.com/in/java/technologies/downloads/)

### Downloading Scala:
[https://www.scala-lang.org/download/](https://www.scala-lang.org/download/)

### Downloading Spark:
[https://spark.apache.org/downloads.html](https://spark.apache.org/downloads.html)

The above downloaded spark file will be in ***.tgz format***, hence we need to extract it. We can directly extract it by ***doing a double click***.

### Setting the environment variables (most important):

Open the terminal and type
```
nano .zshrc
```
It will open an area where we can add the path variables

```
export JAVA_HOME=<path to Java sdk>
export SCALA_HOME=<path to Scala file>
export SPARK_HOME=<path to the extrcated Spark file>
export PATH=$PATH:$SPARK_HOME/bin
```

Now after we are done with setting up the environment variables, its time to reload the configuration:
```
source `/.zshrc
```

#### Now move to the directory where the extracted Spark file is located
```
spark-shell
```
