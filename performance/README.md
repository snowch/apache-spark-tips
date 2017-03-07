### Overview

This document contains tips for performance tuning spark code on IBM's Spark as a Service and IBM's Data Science Experience.

### Table of contents

- [Performance Tuning Process](#performance-tuning-process)
- [Tips](#Tips)
  - [Reading/Writing from Bluemix Object Storage (Swift)](#readingwriting-from-bluemix-object-storage-swift)
  - [Reading/Writing from Softlayer Account Object Storage (Swift)](#readingwriting-from-softlayer-account-object-storage-swift)
  - [Reading from dashDB](#reading-from-dashdb)
    - [Optimizing data reading for dashDB MPP](#optimizing-data-reading-for-dashdb-mpp)
  - [Memory Usage](#memory-usage)


### Performance Tuning Process

 - Navigate to the Spark service in Bluemix
 - Click `Job History`
 - More info coming soon ...


### Tips

#### Reading/Writing from Bluemix Object Storage (Swift)

Use the following library to ensure optimal performance: https://github.com/ibm-cds-labs/ibmos2spark

#### Reading/Writing from Softlayer Account Object Storage (Swift)

Use the following library to ensure optimal performance: https://github.com/ibm-cds-labs/ibmos2spark

#### Reading from dashDB

##### Optimizing data reading for dashDB MPP

Spark provides mechanisms to read data in parallel. When you already have a partitioned data backend such as a dashDB MPP instance, then it makes sense to read the individual data partitions in parallel into Spark. This saves a lot of reshuffling work that would otherwise have to be performed under the hood.

Here is how you can specify that reading happens in parallel along the lines of the dashDB MPP partitions:

```
var df = spark.read.
format("jdbc").
option("url", "jdbc:db2://<DB2 server>:<DB2 port>/<dbname>").
option("user", "<username>").
option("password", "<password>").
option("dbtable", "<your table>").
option("partitionColumn", "DBPARTITIONNUM(<a column   name>)").
option("lowerBound", "<lowest partition number>").
option("upperBound", "<largest partition number>").
option("numPartitions", "<number of partitions>").
load()
```

In case you don't know the partitioning of your dashDB MPP system, here is how you can find it out using SQL:

```
SELECT min(member_number), max(member_number),    count(member_number) 
FROM TABLE(SYSPROC.DB_MEMBERS())
```

Source: https://apsportal.ibm.com/blog/working-with-dashdb-in-data-science-experience/

#### Memory Usage

If you are working on a filtered dataset and do not need to use the unfiltered dataset caching after applying the filter will result in less memory usage:

http://stackoverflow.com/questions/42633757/spark-parquet-query-performance

