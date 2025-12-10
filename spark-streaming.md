---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-08"

keywords: lakehouse, engine, watsonx.data
subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}


# Run Spark Streaming applications
{: #spark-streaming}

Spark Streaming enables scalable, high-throughput, fault-tolerant stream processing of live streams of data, for example from log files or status update messages. HDFS directories, TCP sockets, and Kafka are some of the supported Spark Streaming data sources. The machine learning and graph processing methods in Spark can even be used on data streams and the processed data can be stored in databases and files.
{: .shortdesc}

Spark Streaming takes live input data streams and breaks the streams up into batches, which are processed by the Spark engine to provide a final batch of results. For details, see the [Apache Spark Streaming Programming Guide](https://spark.apache.org/docs/latest/streaming-programming-guide.html){: external}.


## Integrating with Kafka
{: #spk_stream_1}

{{site.data.keyword.lakehouse_short}} supports Kafka as a data source for real-time data streaming. The data is processed as it is streamed and can be stored in HDFS, databases or dashboards. 

This section shows you how you can leverage Spark Streaming on {{site.data.keyword.lakehouse_short}} with Kafka in a sample application called `kafka-stream-example.py`.


Sample Python Spark Streaming application:

```bash
#!/usr/bin/env python
# coding: utf-8

import pyspark
from pyspark.sql import SparkSession
from pyspark.sql.functions import*
from pyspark.sql.types import*
import time

#create spark session
spark = SparkSession.builder.getOrCreate()

# Connect to kafka server and read data stream
df = spark \
.readStream \
.format("kafka") \
.option("kafka.bootstrap.servers", "CHANGEME_KAFKA_SERVER") \
.option("kafka.sasl.jaas.config","org.apache.kafka.common.security.plain.PlainLoginModule required username='CHANGEME_USERNAME' password='CHANGEME_PASSWORD';") \
.option("kafka.security.protocol", "SASL_SSL") \
.option("kafka.sasl.mechanism", "PLAIN") \
.option("kafka.ssl.protocol", "TLSv1.2") \
.option("kafka.ssl.enabled.protocols", "TLSv1.2") \
.option("kafka.ssl.endpoint.identification.algorithm", "HTTPS") \
.option("subscribe", "CHANGEME_TOPIC") \
.load() \
.selectExpr("CAST(key AS STRING)", "CAST(value AS STRING)")

df.printSchema()

# Write the input data to memory
query = df.writeStream.outputMode("append").format("memory").queryName("testk2s").option("partition.assignment.strategy", "range").start()

query.awaitTermination(30)

query.stop()

query.status

# Query data
test_result=spark.sql("select * from testk2s")
test_result.show(5)

spark.sql("select count(*) from testk2s").show()
test_result_small = spark.sql("select * from testk2s limit 5")
test_result_small.show()
```
{: .codeblock}

## Running your Spark applications
{: #spk_stream_2}

To run the Spark application `kafka-stream-example.py` using data that is streamed through Kafka, you need to preload the required Kafka and Spark streaming libraries to Spark. 

{{site.data.keyword.lakehouse_short}} offers multiple options to persist any libraries that you might need in your applications, including your application file.

In the following example, you will upload the required libraries and the Spark application file to a storage.

To run the Spark application `kafka-stream-example.py`:

1. Download the following Python packages from Maven:

{%comment%}

| Package name     | Spark version  | Download link          |
| ---------------- | ---------------|----------------------- |
| `spark-sql-kafka` | 3.2.1 |[spark-sql-kafka-0-10_2.12-3.0.2.jar](https://mvnrepository.com/artifact/org.apache.spark/spark-sql-kafka-0-10_2.12/3.2.1){: external}|
| `spark-streaming-kafka` | 3.2.1 |[spark-streaming-kafka-0-10-assembly_2.12-3.0.2.jar](https://mvnrepository.com/artifact/org.apache.spark/spark-sql-kafka-0-10_2.12/3.2.1){: external} |
| `commons-pool2` | 3.2.1 |[commons-pool2-2.11.1.jar](https://mvnrepository.com/artifact/org.apache.commons/commons-pool2/2.11.0){: external} |

{%endcomment%}

    - `spark-sql-kafka`; Spark version 3.3; download from [spark-sql-kafka-0-10_2.12-3.3.0.jar](https://mvnrepository.com/artifact/org.apache.spark/spark-sql-kafka-0-10_2.12/3.3.0){: external}
    - `spark-streaming-kafka`; Spark version 3.3; download from [spark-streaming-kafka-0-10-assembly_2.12-3.3.0.jar](https://mvnrepository.com/artifact/org.apache.spark/spark-streaming-kafka-0-10-assembly_2.12/3.3.0){: external}
    - `commons-pool2`; Spark version 3.3; download from [commons-pool2-2.11.1.jar](https://mvnrepository.com/artifact/org.apache.commons/commons-pool2/2.11.0){: external}

1. Upload the packages and the Spark application file to the storage:

1. Prepare the Spark application payload.

    You need to define the `storage` section in the payload and add the storage and mount details to load the required Python packages before the Spark application starts.

    In the following sample `payload.json`, the Spark application `kafka-stream-example.py` and the Kafka libraries are stored in the `data-vol` volume that is mounted to `s3a://my-bucket/`. The Python application and the comma-separated list of JARs included in the `jars` option are automatically transferred to the cluster. 

    ```bash
    {
       "application_details": {
           "application": "s3a://my-bucket/kafka-stream-example.py",
           "conf": {
               "spark.app.name": "SparkStreams",
               "spark.eventLog.enabled": "true"
           },
           "jars": "s3a://my-bucket/spark-sql-kafka-0-10_2.12-3.3.0.jar,s3a://my-bucket/spark-streaming-kafka-0-10-assembly_2.12-3.3.0.jar,s3a://my-bucket/commons-pool2-2.11.1.jar"
       }
   }
    ```
    {: .codeblock}

1. Submit the PySpark application. For details, see [Submitting Spark jobs via API](/docs/watsonxdata?topic=watsonxdata-smbit_nsp_1).
