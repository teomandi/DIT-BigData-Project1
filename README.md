# Project 1
Big Data subject.
- Implemented by:
   - Theodoros Mandilaras
   - cs2.190018
- MSc DIT/EKPA 2019-2020

---

## Simple Statistics in Scala

Firstly we load the  csv like:
```
scala> val df - spark.read.options( Map("header"-> "true", "escape"-> "\"", "inferSchema"-> "true")).csv("/absolute/path/to/fake_job_postings.csv")
```
### a 
Number of lines in the CSV file
```
scala> df.count()

res0: Long = 17881
```
### b
Number of fake job postings
```
scala> val fake_jobs = df.filter("fraudulent == 1")
scala> fake_jobs.count()

res5: Long = 866
```
### c
Number of real job postings
```
scala> val real_jobs = df.filter("fraudulent == 0")
scala> real_jobs.count()

res5: Long = 17014
```
### d
Top-10 most required education (e.g. Bachelor’s Degree) in fake job postings
```
scala> fake_jobs.groupBy("required_education").count().sort($"count".desc).show(10)

+--------------------+-----+
|  required_education|count|
+--------------------+-----+
|                null|  451|
|High School or eq...|  170|
|   Bachelor's Degree|  100|
|         Unspecified|   61|
|     Master's Degree|   31|
|Some High School ...|   20|
|       Certification|   19|
|    Associate Degree|    6|
|        Professional|    4|
|Some College Cour...|    3|
+--------------------+-----+
only showing top 10 rows
```

### e 
Top-10 most required education in real job postings
```
scala> real_jobs.groupBy("required_education").count().sort($"count".desc).show(10)
+--------------------+-----+
|  required_education|count|
+--------------------+-----+
|                null| 7654|
|   Bachelor's Degree| 5045|
|High School or eq...| 1910|
|         Unspecified| 1336|
|     Master's Degree|  385|
|    Associate Degree|  268|
|       Certification|  151|
|Some College Cour...|   99|
|        Professional|   70|
|          Vocational|   49|
+--------------------+-----+
only showing top 10 rows

```