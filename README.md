#### Installing Spark

```bash
export JAVA_HOME=/opt/homebrew/Cellar/openjdk@17/17.0.14
export PATH="$JAVA_HOME/bin/:$PATH"

export SPARK_HOME=/opt/homebrew/Cellar/apache-spark/3.5.5/libexec
export PATH="$SPARK_HOME/bin/:$PATH"

export PYTHONPATH="${SPARK_HOME}/python/:$PYTHONPATH"
export PYTHONPATH="${SPARK_HOME}/python/lib/py4j-0.10.9.5-src.zip:$PYTHONPATH"
```

#### Testing Spark
```python
import pyspark
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \
    .appName('test') \
    .getOrCreate()

df = spark.read \
    .option("header", "true") \
    .csv('taxi_zone_lookup.csv')

df.show()

df.write.parquet('zones')
```