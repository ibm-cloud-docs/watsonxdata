---

copyright:
  years: 2017, 2025
lastupdated: "2025-10-28"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with watsonx.ai Notebooks
{: #run_nbwxai}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

{{site.data.keyword.lakehouse_full}} integrates with watsonx.ai to allow a web-based working experience with Jupyter Notebook. You can use the watsonx.ai interface to build your own code in the Jupyter Notebook, and run it by using watsonx.data Spark as the runtime environment.
{: shortdesc}


For more information about Jupyter Notebook, see [Notebooks](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/notebooks-and-scripts.html?context=wx&audience=wdp).

## Prerequisites
{: #spk_nb_preqwxai}

Subscription to watsonx.ai on IBM Cloud.


## Procedure
{: #Spk_nb_procwxai}

To run the Jupyter Notebook on your watsonx.data spark engine, do the following:

1. Create watsonx.ai project. To create a watsonx.ai project, see [Creating a project](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/projects.html?context=wx&audience=wdp).

2. Create a Spark engine environment. To run a Jupyter Notebook, you must create a runtime environment template.

   To do that, access the watsonx. ai project from the UI. Go to **Manage** tab. Create a template. For more information about creating environment templates, see [Creating environment templates](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/create-customize-env-definition.html?context=wx&audience=wdp). While creating the template, select **Type** as **Spark** and from the **Spark** engine list, select the native Spark engine that you provisioned in the watsonx.data instance.


3. Create a Jupyter Notebook asset and access it from the Jupyter Notebook editor tool. To create a notebook file in the notebook editor, see [Creating a notebook file in the notebook editor](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/creating-notebooks.html?context=wx&audience=wdp#file).

   When you create the notebook, specify the runtime environment that you created for the watsonx.data spark engine.

   The notebook opens in edit mode. You can start working on it. For more information, see [Creating a notebook file in the notebook editor](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/creating-notebooks.html?context=wx&audience=wdp#file).

## Accessing the watsonx.data catalog
{: #Spk_nb_procwxai_catlg}

Add the following code snippet in the notebook cell and run it. The code snippet includes configurations that are required to connect to the associated watsonx.data catalog.


   ```bash
   conf=spark.sparkContext.getConf()
   spark.stop()

   from pyspark.sql import SparkSession
   from pyspark.sql.functions import col, to_utc_timestamp
   import base64,getpass

   wxd_username=getpass.getpass("Please enter your username with hms access:").strip() #Prompt for username
   wxd_hms_username="ibmlhapikey_"+wxd_username
   wxd_hms_password=getpass.getpass("Please enter your api key with hms access:").strip() #Prompt for api key
   string_to_encode= wxd_hms_username+":"+wxd_hms_password
   wxd_encoded_apikey="Basic " + base64.b64encode(string_to_encode.encode("utf-8")).decode("utf-8")

   conf.setAll([("spark.hive.metastore.client.plain.username", wxd_hms_username), \
       ("spark.hive.metastore.client.plain.password", wxd_hms_password), \
       ("spark.hadoop.wxd.apikey", wxd_encoded_apikey)
   ])

   spark = SparkSession.builder.config(conf=conf).enableHiveSupport().getOrCreate()
   ```
   {: codeblock}




   You can step through the notebook execution cell, by selecting **Shift-Enter** or you can run the entire notebook. It prompts for the username and password.
   Username is the IBM Cloud ID of the user whose api key is used to access the data bucket. The API Key here is the API key of the user accessing the Object storeage. To generate an API key, log in into the watsonx.data console and navigate to **Profile > Profile and Settings > API Keys** and generate a new API key.


You can add more code snippets based on your use case and continue. For more information, see [Creating a notebook file in the notebook editor](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/creating-notebooks.html?context=wx&audience=wdp#file).
{: note}
