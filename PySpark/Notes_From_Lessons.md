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





# Lesson 
## 

# Lesson 
## 