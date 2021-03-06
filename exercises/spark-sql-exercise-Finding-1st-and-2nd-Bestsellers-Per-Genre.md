# Exercise: Finding 1st and 2nd Bestsellers Per Genre (Spark SQL)

## Input Dataset

```text
id,title,genre,quantity
1,Hunter Fields,romance,15
2,Leonard Lewis,thriller,81
3,Jason Dawson,thriller,90
4,Andre Grant,thriller,25
5,Earl Walton,romance,40
6,Alan Hanson,romance,24
7,Clyde Matthews,thriller,31
8,Josephine Leonard,thriller,1
9,Owen Boone,sci-fi,27
10,Max McBride,romance,75
```

```text
val books = spark
  .read
  .option("header", true)
  .option("inferSchema", true)
  .csv("book_sales.csv")
scala> books.show
+---+-----------------+--------+--------+
| id|            title|   genre|quantity|
+---+-----------------+--------+--------+
|  1|    Hunter Fields| romance|      15|
|  2|    Leonard Lewis|thriller|      81|
|  3|     Jason Dawson|thriller|      90|
|  4|      Andre Grant|thriller|      25|
|  5|      Earl Walton| romance|      40|
|  6|      Alan Hanson| romance|      24|
|  7|   Clyde Matthews|thriller|      31|
|  8|Josephine Leonard|thriller|       1|
|  9|       Owen Boone|  sci-fi|      27|
| 10|      Max McBride| romance|      75|
+---+-----------------+--------+--------+
```

NOTE: Use [Online Generate Test Data](http://www.convertcsv.com/generate-test-data.htm) for more sophisticated datasets in CSV or JSON format.

## Expected Dataset

```text
scala> solution.show
+---+-------------+--------+--------+----+
| id|        title|   genre|quantity|rank|
+---+-------------+--------+--------+----+
| 10|  Max McBride| romance|      75|   1|
|  5|  Earl Walton| romance|      40|   2|
|  3| Jason Dawson|thriller|      90|   1|
|  2|Leonard Lewis|thriller|      81|   2|
|  9|   Owen Boone|  sci-fi|      27|   1|
+---+-------------+--------+--------+----+
```

Duration: **30 mins**

<!--
## Solution

```text
import org.apache.spark.sql.expressions.Window
val genreByQuantityDesc = Window.partitionBy("genre").orderBy($"quantity".desc)
val solution = books.withColumn("rank", rank over genreByQuantityDesc).filter($"rank" < 3)
```

-->
