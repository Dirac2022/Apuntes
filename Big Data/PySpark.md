
# Introduction to PySpark

## Introduction to Apache Spark and PySpark

### Introduction to PySpark

- Distributed data processing: Designed to handle large datasets across clusters.
- Supports varios data formats including CSV, Parquet, and JSON.
- SQL integration allows querying of data using both Python and SQL syntax.
- Optimized for speed at scale.

<h5>Spark cluster</h5>

[[Apache Spark#Arquitectura de una Aplicación Spark|Arquitectura de una Aplicacion Spark]]


**Master Node**
- Manages the cluster, coordinates tasks and schedules jobs

**Worker Nodes** ([[Apache Spark#Worker Nodes|Worker Nodes]])
- Execute the tasks assigned by the master.
- Responsible for executing the actual computations and storing data in memory or disk.


#### `SparkSession`

`SparkSession` allow you to access your Spark cluster and are critical for using PySpark

```python
from pyspark.sql import SparkSession

# Initialize a SparkSession
spark = SparkSession.builder.appName("MySparkApp").getOrCreate()
```

- `builder()` : sets up a session.
- `getOrCreate()` : creates or retrieves a session.
- `appName()` : helps manage multiple sessions.


#### PySpark DataFrames

Optimized DataFrames for PySpark

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('MySparkApp').getOrCreate()

# Create a DataFrame
census_df = spark.read.csv("census.csv", ['gender', 'age', 'zipcode', 'salary_range_usd', 'marriage_status'])

# Show the DataFrame
census_df.show()
```


> [!tip] `spark.read.csv`
> `spark.read.csv()` reads CSV files into a `DataFrame`. You can let Spark infer column types with `inferSchema=True`.
> 
> **Signature:**
> 
> ```python
> DataFrameReader.csv(path, schema=None, sep=',', header=False, inferSchema=False)
> ```
> 
> * **path** *(str or list)*: file path(s).
> * **schema** *(StructType or str)*: optional schema.
> * **sep** *(str)*: field delimiter.
> * **header** *(bool)*: first row as column names.
> * **inferSchema** *(bool)*: infers column types from data.
> 
> **Examples:**
> 
> ```python
> df = spark.read.csv("data/file.csv", header=True, inferSchema=True)
> df = spark.read.csv("data/file.csv", sep=";", header=True, inferSchema=True)
> ```



<h5> Creating DataFrames from filestores</h5>

```python
census_df = spark.read.csv('path/census.csv', header=True, inferSchema=True)

# Show the first 5 rows of the DataFrame
census_df.show()
```

|     | age | education.num | marital.status | occupation        | income |
| --: | --: | ------------: | :------------- | :---------------- | :----- |
|   0 |  90 |             9 | Widowed        | ?                 | <=50K  |
|   1 |  82 |             9 | Widowed        | Exec-managerial   | <=50K  |
|   2 |  66 |            10 | Widowed        | ?                 | <=50K  |
|   3 |  54 |             4 | Divorced       | Machine-op-inspot | <=50K  |
|   4 |  41 |            10 | Separated      | Prof-specialty    | <=50K  |

<h5> Printing DataFrame Schema</h5>
```python
# Show the schema 
census_df.printSchema() 
Output: 
root 
|-- age: integer (nullable = true) 
|-- education.num: integer (nullable = true) 
|-- marital.status: string (nullable = true) 
|-- occupation: string (nullable = true) 
|-- income: string (nullable = true) 
```


<h5>Basic analytics on PySpark DataFrames</h5>
- `count()` : will return the total row numbers in the DataFrame
- `groupBy()` : allows the use of sql-like aggregations
- Other aggregate functions: `sum()`, `min()`, `max()`

```python
row_count = census_df.count()
census_df.groupBy('gender').agg({'salary_usd': 'avg'}).show()
```


<h5>Key functions for PySpark analytics</h5>
- `select()` : Selects specific columns from the DataFrame.
- `filter()` : Filters rows based on specific conditions. 
- `groupBy()` : Group rows based on one or more columns.
- `agg()` : Applies aggregate functions to grouped data.

Example:

```python
 # Using filter and select, we can narrow down our DataFrame 
filtered_census_df = census_df.filter(df['age'] > 50).select('age', 'occupation') 
filtered_census_df.show()  

# Output 
+---+------------------+ 
|age|       occupation | 
+---+------------------+ 
| 90|                 ?| 
| 82|   Exec-managerial| 
| 66|                 ?| 
| 54| Machine-op-inspct| 
+---+------------------+ 
```


> [!note] `where()`
> In PySpark `filter()` and `where()` are functionally equivalent; `where()` is just an alias for `filter()`. 
>
> Examples:
>
> ```python
> df.filter(df.age > 30)
> df.where("age > 30")
> ```


<h5>Spark DataFrames</h5>

We can create DataFrames from various data sources

- CSV files : `spark.read.csv('path/file.csv')`
- JSON files : `spark.read.json('path/file.csv')`
- Parquet Files : `spark.read.parquet('path/file.csv')`


#### DataTypes in PySpark DataFrames

These are the most basic types, representing a single value.

* **`StringType`**: Character strings. Corresponds to Python's `str`.
    * **Example**: `"Madrid"`, `"Product A"`
    
* **`IntegerType`**: 32-bit signed integers. Corresponds to Python's `int`.
    * **Example**: `25`, `1000`
    
* **`LongType`**: 64-bit signed integers. Used for large integers and is the default for `int` in many cases.
    * **Example**: `9876543210`
    
* **`DoubleType`** and **`FloatType`**: Floating-point numbers for decimal values.
    * **Example**: `19.99`, `3.14159`
    
* **`BooleanType`**:  `True`, `False`
	
* **`DateType`**: Dates only. Corresponds to Python's `datetime.date`.
    * **Example**: `date(2024, 7, 25)`
* **`TimestampType`**: Dates and times with timezone information. Corresponds to Python's `datetime.datetime`.
    * **Example**: `datetime(2024, 7, 25, 10, 30, 0)`


Complex Data Types

These are used to structure nested data or collections.

* **`ArrayType`**: A collection of elements of the same type. It is equivalent to a Python list.
    * **Example**: For a tags column: `["marketing", "digital", "social media"]`
    
* **`MapType`**: A collection of key-value pairs. It is equivalent to a Python dictionary.
    * **Example**: For a metrics column: `{"clicks": 1500, "impressions": 25000}`
    
* **`StructType`**: Used to create nested structures (like an "object" inside another). A `StructType` contains several `StructField`s, where each `StructField` defines a nested column with its name, data type, and nullability.
    * **Example**: For an `address` column: `{"street": "Main Street", "number": 101, "city": "Lima"}`

<h5>DataTypes Syntax for PySpark DataFrames</h5>

```python
from pyspark.sql.types import (StructType, 
                              StructField, IntegerType, 
                              StringType, ArrayTipe)


# Construct the schema
schema = StructType([
    StructFlied('id', IntegerType(), True),
    StructFlied('name', StringType(), True),
    StructFlied('scores', ArrayType(IntegerType()), True),
])

# Set the schema
df = spark.createDataFrame(data, schema=schema)
```


<h5>Sorting and dropping missing vallues</h5>

-  Order data using  `.sort()` or `.orderBy()`
 - Use  `na.drop()` to remove rows with null values


```python
# Sort using the age column 
df.sort("age", ascending=False).show() 

# Drop missing values 
df.na.drop().show() 
```


## PySpark in Python





## Introduction to PySpark SQL