# learn_spark
Central to Spark are RDDs - Resilient Distributed Datasets. Spark distributes the RDD for parallel processing and they encapsulate a dataset.
Two main operations are done on an RDD:
1. Transformation
2. Action

## Typical Spark workflow
1.Generate initial RDDs from external data.
2.Apply transformations.
3.Launch actions.

## Creating an RDD
### Take an existing collection in your program and pass it to SparkContext's parallelize method.

List<Integer> inputIntegers = Arrays.asList(1,2,3,4,5);
JavaRDD<Integer> integerRDD = sc.parallelize(inputIntegers);

Once this is done, integerRDD would be an RDD that can be operated on in parallel.

Practically not possible as the size of dataset is very large typicall and this approach needs that dataset to be loaded in memory ( heap ), which is not possible.

### Load RDDs from external storage by calling textFile method on SparkContet.

JavaSparkContext cc = new JavaSparkContext(conf);
JavaRDD<String> lines = sc.textFile( "in/uppercase.text" );
  
External storage can be Amazon S3 or HDFS. It can even be Elastic Search, Cassandra, JDBC.

Spark JDBC driver:
https://docs.databricks.com/spark/latest/data-sources/sql-databases.html

Spark Cassandra connector:
http://www.datastax.com/dev/blog/kindling-an-introduction-to-spark-with-cassandra-part-1

Spark Elasticsearch connector:
https://www.elastic.co/guide/en/elasticsearch/hadoop/current/spark.html

## Transformations
Returns a new RDD instead of mutating the existing RDD.
1. filter() - used for getting a subset of the RDD.
2. map() - lets each element in the input RDD pass through the function that it takes. Can also make HTTP calls.
