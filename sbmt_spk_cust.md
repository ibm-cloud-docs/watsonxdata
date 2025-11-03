---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-28"

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

# Customizing parameters for Spark application submission
{: #sbmt_spk_cust}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}


This topic explains how to configure the Spark application payload to include idempotency keys, and set maximum runtime controls when submitting a Spark application in watsonx.data.
{: shortdesc}

When submitting a Spark application in watsonx.data, you can customize the application payload to include the following features:

Idempotency keys: It ensures that application submissions are processed exactly once, even in cases of client-server communication failures.
Consider an example where you are submitting a Spark application. Due to a temporary network issue between your client and the server, the request times out and you don’t receive a confirmation. Unsure whether the job was successfully submitted, you retry the submission multiple times. Each retry creates a new application ID, resulting in multiple instances of the same job running potentially consuming unnecessary resources. To avoid this, you can include an Idempotency key in your application payload. This key acts as a unique identifier for the job submission. If you resubmit the same application with the same idempotency key, multiple requests with the same idempotency key are treated as a single submission.



Maximum runtime controls: You can define a maximum execution time for Spark applications. If the timeout is not specified, jobs continues to run until completion, regardless of how long they take.


## Configuring Idempotency key in payload
{: #sbmt_spk_cust-idmptncy}

Use the idempotency_key parameter in the Spark application payload to avoid triggering duplicate job submissions. This ensures that repeated requests with the same key are treated as a single request. Idempotency_key cannot be greater than 64 characters in length.

The following is a sample payload. Specify the idempotency_key parameter value in the <userdefined_key> field while submitting an application.
cat idempotency_test.json

   ```bash
   {
     "application_details": {
       "application": "/opt/ibm/spark/examples/src/main/python/wordcount.py",
       "arguments": [
         "/opt/ibm/spark/examples/src/main/resources/people.txt"
       ],
       "conf": {
         "spark.app.name": "PySpark Application",
         "spark.eventLog.enabled": "true"
       }
     },
     "idempotency_key": "<userdefined_key>"
   }
   ```
   {: codeblock}

## Configuring maximum runtime time in payload
{: #sbmt_spk_cust-mxrun}

Use the timeout_in_seconds parameter in the payload to specify the maximum execution time while submitting an application.

The following is a sample payload that shows how to configure the timeout_in_seconds while submitting an application. Here, the maximum execution time is 10 seconds. If the timeout is not specified, jobs will continue to run until completion, regardless of how long they take.


   ```bash
   {
       "application_details": {
                   "application":"cos://uma-cos-1.mycos/longrunning_with_sleep.py",
       "conf": {
         "spark.app.name": "cosApp",
         "spark.hadoop.fs.cos.mycos.endpoint": "s3.us-south.cloud-object-storage.appdomain.cloud",
         "spark.hadoop.fs.cos.mycos.secret.key": "fbf6bcc31eb2bf85ebd02949edf26cf893a9256bcfa91ebe",
         "spark.hadoop.fs.cos.mycos.access.key": "73976d45c75e4d548381e4da0e98f816"
       }
           },
       "timeout_in_seconds":"60"
   }'
   ```
   {: codeblock}


