# Lesson 1
## PySpark - Zero to Hero | Introduction | Learn from Basics to Advanced Performance Optimization

### What is Spark

Spark is an Open Source UNified Computing Engine with set of libraries for parallel data processing on compute cluster. It processes data in memory(RAM) which makes it 100 times faster than traditinal Haddop Map Reduce.


# Lesson 2
## How Spark Works - Driver & Executors | How Spark divide Job in Stages | What is Shuffle in Spark

![Spark Workflow](image.png)

### What are Drivers and Executers
An instructor process is the __Driver__ in a Spark job. A worker process is the __Executor__ in a spark job.

A __shuffel__ is when data is persisted and shared to other executors. 

Driver role:
- Heart of the Spark Application
- Manages the information and state of executors
- Analyzes, distributes and Schedules the work on executors

Executor role:
- Execute the code
- Report the status of execution to driver

# Lesson 3
## Spark Transformations & Actions | Why Spark prefers Lazy Evaluation |What are Partitions in Spark

### What is Partition
To allow executors to work in parallel, Spark breaks down the data into chunks called partitions. 


### What are Transformation
The instruction or code to modify and transform data is knoen as Transformation. Eg. select, where, groupBy etc.
Two types exist: 
1. Narrow Transformation
    - After applying transformation each partition contribute to at-most one partition
2. Wide Transformation
    - After applying transformation if one partition contribute to more than one partition. This type of transformation leads to data shuffle.

### What are Actions
To trigger an execution we need to call an Action (due to lazy evaluation). This executes the plan created by the Transformations.

Three type of Actions exist:
1. View data in console
2. Collect data to native language
3. Write data to output data sources

### What is Spark Session
The Driver process is knoen as Spark Session, this is the entry point for a spark session. The Spark Session instance executes the code in the cluster. Each spark application has its own Spark session.


# Lesson  4
## Spark DataFrames & Execution Plans | Spark Logical and Physical Execution Planning | What are DAG


# Lesson 5
## Understand Spark Session & Create your First DataFrame | Create SparkSession object | Spark UI


# Lesson 6
## Basic Structured Transformation - Part 1 | Write Spark DataFrame Schema |Ways to write DF Columns


### Spark Hands on

`dataframe.printSchema()` will show a tree format schema summary of the dataframe schema.  
`dataframe.schema()` will show the schema through SrtuctType and StructField objects. Also, the column name, the data type and wether it is nullable field is presented.

Exmaple on Spark Schema:
```
from pyspark.sql.types import StryctType, StructField, StringType, IntegerType
schema_string = "name string, age int"

schema_spark = Structtype([
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])
```

#### DataFrame Schema - Structured Trasnfroamtions - select, expr, selectExpr, cast

Columns and expressions
```
from pyspark.sql.functions import col, expr

col("name") // any mainpulation done on a dataframe is evalauted as an expression

expr("name") // will result as the same as the above line

dataframe.salary // will result in the above

dataframe["salary"] // will result in the same
```

SELECT Columns
```
dataframe_filtered = emp.select(col("column_name"), expr("column_name"), dataframe.column)
```

Show Dataframe
```
dataframe_filtered.show()
```

Using expr for Select
```
dataframe_casted = dataframe_filtered.select(expr("column_name as col_name"), dataframe_filtered.column_name, expr("cast(column_name as int) as column_name_v2"))
```

Using Select + expr = selectExpr
```
df_casted = dataframe.selectExpr("column_name_0 as col_name_0", "column_name", "cast(column_name_1 as int) as col_name_1", "column_name_2")
``` 

Filter 
```
df_filtered = dataframe.select("column_name").where("column_name > 30")
```

Write to csv
```
dataframe.write.format("csv").save("path_to_file")
```

Schema definition through strings
```
schema_str = "name string, age int"

from pyspark.sql.types import _parse_datatype_string

schema_spark = _parse_datatype_string(schema_str)
```


# Lesson 7
## Basic Structured Transformation - Part 2 | Cast Column | Add Column | Static Column Value |Rename

### Spark Hands on

Adding Columns in Spark
```
df_added = df.withColumn("new_column", col("column_name") * 0.2)
// withColumn lets you add or update an old column

// adding several new columns with lit values
columns = {
    "col_0" : lit(0),
    "col_1" : lit(1),
    "col_2" : lit(2),
}

df = df.withColumns(columns)
```

Static values | literals
```
import pyspark.sql.functions import lit

df_new_cols = df.withColumn("col1", lit(1)).withColumn("col2", lit(2)) 
``` 

Rename columns
```
df = df.withColumnRenamed("old_column_name", "new_column_name")
```

Remove columns
```
df = df.drop("column_name", "column_name_1")
```

# Lesson 8
## Working with Strings, Dates and Null | Regex Replace | Convert string to date | Transform NULL

### Spark Hands on

When operation
```
from pyspark.sql.functions import when

df = df.withColumn("col_name", when(col("g") == "m", "M")
                                .when(col("g") == "f", "F")
                                .otherwise(None))
``` 

Convert Date
```
from pyspark.sql.functions import to_date

df = df.withColumn("date_column", to_date(col(date_column), "yyyy-mMM-dd"))
```

NA operations
```
// drop NA
df = df.na.drop()

// replace NA
from pyspark.sql.functions import coalesce, lit
df = df.withColumn("column_name", coalesce(col("column_name"), lit(O)))
// cannot write string directly, need to use literals
```


# Lesson 9
## Sorting data, Union and Aggregation in Spark | Difference in Union and UnionAll | Having Clause

### Spark Hands on


# Lesson 10
## Window Functions, Unique Data & Databricks Community Cloud | Second Highest Salary | Spark expr

### Spark Hands on

Window funtions
```
from pyspark.sql.window import Window
from pyspark.sql.functions import max, col, desc

window_spec = Window.partitionBy(col("column_name")).orderBy(col("column_name_1").desc())
max_func = max(col("column_name_1")).over(window_spec)

df = df.withColumn("max_column_name_1", max_func)
```


# Lesson 11
## Data Repartitioning & PySpark Joins | Coalesce vs Repartition | Spark Data Partition | Joins

### Spark Hands on

#### Partition
Spark operates by data being divided into partitions. To query for the number of partitions a datafram is divided into use: 
```
df.rdd.getNumPartitions()
```
To repartition the dataframe use:
```
df = df.repartition(n_partitions)
```
Coalesce vs REpartitions
Repartition involves data shuffel, wheras Coalsces dosen't. Repartition can increase or decrease partition numbers but, Coalsces can only decrese no increase. Repartition allows unifrom data distribution, but Coalsces can't guaranree it.  

Partition Id
```
from pyspark.sql.functions import spark_partition_id

spark_partition_id // this variable will return the partition id
```

#### Joins



# Lesson 12
## Understand Spark UI, Read CSV Files and Read Modes | Spark InferSchema Option | Drop Malformed

### Read CSV Data
Spark can read from a csv file. Reading in Spark is a transformation, not an action. Hence, when performing a read on a csv file, spark should not run a job. However, spark will run a single task in order to acquire metadata. Depending on what options are enabled, spark will acquire more metadata, for instance; schema inference.

```
df = spark.read.format("csv").option("header", True).options("inferSchema", True).load("file/path")
``` 

If schema is defined during data load, spark will not perform a job during load. Since no metadata is required. This is importent in production systems to reduce overhead.
```
_schema = "..."

df_schema = spark.read.format(csv).schema(_schema).load("file/path")
```

#### Mode in data load

Mode is an option during data load that will allow to configure data load behaviour. This option requires the schema to be defined pre load. Modes that exist: [PERMISSIVE, DROPMALEFORMED, FAILFAST]

Spark has an inbuilt column `_corrupt_record`, with datatype string, which must be defined during schema definition for it to be used. Howver the column name is not mandatory, this can be given a custom value in an option statement.

PERMISSIVE   
By defualt the PERMISSIVE mode is used. When `_corrupt_record` is defined in the schema, spark will populate this with the corrupt records.
```
df_p = spark.read.format("csv").schema(_schema).option("header", True).load("file/path")

// renaming the _corrupt_record column name. The chosen name needs to be defined in the schema.
df_p = spark.read.format("csv").schema(_schema).option("header", True).option("columnNameOfCorruptRecord", "bad_record")load("file/path")
```

DROPMALEFORMED  
This mode will drop the records that have bad_records.
```
df_m = spark.read.format("csv").schema(_schema).option("header", True).option("mode", "DROPMALEFORMED").load("file/path")
```

FAILFAST   
In the other examples either the bad_record was included, or it was dropped. Eitherway the job ran without an error. FAILFAST mode will fail the job as soon as a Bad Record is identified.
```
df_f = spark.read.format("csv").schema(_schema).option("header", True).option("mode", "FAILFAST").load("file/path")
```

#### Multiple options
The `options()` function can be used alongside multiple values to reduce the verbose configuraiton. 
```
_options = {
    "asd":"asd",
    "asd":"asd",
    "asd":"asd"
}

df = (spark.read.format("csv").options(**_options).load("path/to/file"))
```


# Lesson 13
## Read Complex File Formats | Parquet | ORC | Performance benefit of Parquet |Recursive File Lookup



# Lesson 14
## 



