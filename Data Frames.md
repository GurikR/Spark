# Data Frames
Data frames: is a distributed collection of data grouped into named columns
Schema: defines column names and type of a data frame.

DataFrame transformations: are methods that returns dataframes and are lazily evaluated.
eg: 
df.select("id", "result")
  .where("result > 70")
  .orderBy("result")

display(spark.table("products")
  .select("name", "price")
  .where("price < 200")
  .orderBy("price"))

productsDF = spark.table("products")
above statement spark.table return df 
productsDF:pyspark.sql.dataframe.DataFrame
item_id:string
name:string
price:double

resultDF = spark.sql("""
SELECT name, price
FROM products
WHERE price < 200
ORDER BY price
""")

display(resultDF)

budgetDF = (spark.table("products")
  .select("name", "price")
  .where("price < 200")
  .orderBy("price"))
budgetDF.schema - defines column names and types of a dataframe.
eg: Out[12]: StructType([StructField('name', StringType(), True), StructField('price', DoubleType(), True)])
budgetDF.printSchema() - more readable output
root
 |-- name: string (nullable = true)
 |-- price: double (nullable = true)

(productsDF
  .select("name", "price")
  .where("price < 200")
  .orderBy("price")
  .show())
output:
+--------------------+-----+
|                name|price|
+--------------------+-----+
|Standard Foam Pillow| 59.0|
|    King Foam Pillow| 79.0|
|Standard Down Pillow|119.0|
|    King Down Pillow|159.0|

budgetDF.count()
output: 4
budgetDF.collect() 
output:
[Row(name='Standard Foam Pillow', price=59.0),
 Row(name='King Foam Pillow', price=79.0),
 Row(name='Standard Down Pillow', price=119.0),
 Row(name='King Down Pillow', price=159.0)]

**Convert between DataFrames and SQL**
createOrReplaceTempView creates a temporary view based on the DataFrame. The lifetime of the temporary view is tied to the SparkSession that was used to create the DataFrame.

budgetDF.createOrReplaceTempView("budget")
display(spark.sql("SELECT * FROM budget"))
output: table or results


Dataframa actions: are methods that trigger computation.
eg: df.count() - no of records in df, df.collect() - no of rows in df, df.show() - shows top few rows in df

An action is needed to trigger the execution of any transformation
df.select("id", "result")
  .where("result > 70")
  .orderBy("result")
  .show()

# Spark Session
Spark Session: is single entry point to all **dataframe api** functionality, automatically created in databricks notebook as variable **spark**.
<img width="695" alt="Screenshot 2023-08-26 222530" src="https://github.com/GurikR/Spark/assets/5446906/e0825298-0609-4478-a55a-1783427e4155">

# Reader and Writer
DataFrameReader - Interface used to load df from external resources
spark.read.parquet("/mnt/training/ecommerce/events.parquet")

DFWriter - used to write data to external systems.
(df.write()
  .option("compression", "snappy")
  .mode("overwrite")
  .parquet(outPath)
  )



