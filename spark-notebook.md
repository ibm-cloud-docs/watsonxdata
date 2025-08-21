---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-21"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Running Spark notebook from Watson Studio on Cloud Pak for Data
{: #run_nb}


The option to register external Spark engines in watsonx.data is deprecated in this release and will be removed in version 2.3. watsonx.data already includes built-in Spark engines that you can provision and use directly, including the Gluten-accelerated Spark engine and the native watsonx.data Spark engine.
{: important}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

The topic provides the procedure to run a sample Spark application by using Watson Studio notebooks. The notebook resides in a Watson Studio project that is available IBM Cloud Pak for Data (CPD) cluster.
{: shortdesc}

You can download and run the Spark use case sample in Watson Studio to explore the following functions in {{site.data.keyword.lakehouse_short}}:

* Accessing tables
* Loading data
* Modifying schema
* Performing table maintenance activities

Watson Studio provides sample note books that allow to run small pieces of code that process your data, and immediately view the results of your computation. The notebook includes a sample use case that the users can readily download and start working on.
{: note}

## Prerequisites
{: #spk_nb_preq}

* Install Watson Studio on the CPD cluster.

* Retrieve watsonx.data credentials

    Get the following information from watsonx.data:

    * <wxd_hms_endpoint> : Thrift endpoint. For example, thrift://81823aaf-8a88-4bee-a0a1-6e76a42dc833.cfjag3sf0s5o87astjo0.databases.appdomain.cloud:32683. To get the details, log in to your watsonx.data instance, Click on the Iceberg data catalog from Infrastructure manager. In the Details tab, copy Metastore host, which is your <wxd_hms_endpoint>.

    * <wxd_hms_username> : This is by default `ibmlhapikey`.

    * <wxd_hms_password> : Hive Metastore (HMS) password. Get the password from the watsonx.data administrator.

* Source bucket details: If you bring your own Jupiter notebook, you must require the following details of your source bucket where data resides.

    * <source_bucket_endpoint> : Endpoint of the source bucket. For example, for a source bucket in Dallas region, the endpoint is s3.direct.us-south.cloud-object-storage.appdomain.cloud. Use public endpoint.

    * <source_bucket_access_key> : Access key of the source bucket.

    * <source_bucket_secret_key> : Secret key of the source bucket.

* Download the [sample notebook](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/995a90fc-ef89-4fe1-9a1f-092d8be0d839?context=wx).



## Procedure
{: #Spk_nb_proc}

To run the Spark sample notebook, follow the steps:

1. Log in to your Watson Studio account in IBM Cloud Pak for Data cluster.

2. Create a project. For more information, see [Creating a project](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/projects.html?context=cpdaas&audience=wdp).

3. Select the project and add the Jupyter Notebook.

4. Click **New Assets** to create a new asset of Jupyter Notebook. The **New Assets** page opens. For more information, see [Creating notebooks](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/creating-notebooks.html?context=cpdaas&audience=wdp).

5. Click **Code editors**.

6. Search and select **Jupyter Notebook editor**. The New notebook page opens.

7. Specify the following details:
    * Name: Type the name of the notebook.

    * Select the **Spark runtime**. It must be Spark 3.4 with Python 3.10 or 3.11. For other supported Spark versions, see [Supported Spark version](/docs/watsonxdata?topic=watsonxdata-wxd-ae_limits#cpu-mem-spk_versn).

8. Upload and run [IBM published Spark notebook](https://dataplatform.cloud.ibm.com/exchange/public/entry/view/995a90fc-ef89-4fe1-9a1f-092d8be0d839?context=wx). Follow the steps:

    * From the left window, click **Local file**.

    * In the **Notebook file** field, drag the IBM Spark notebook file (that is provided by IBM) from your local computer.

    * Update the watsonx.data credentials, source bucket and catalog bucket details in the **Configuring IBM Analytics Engine** section in the notebook.

9. Click **Create**. The uploaded notebook opens.

10. You can step through the notebook execution cell by cell, by selecting **Shift-Enter** or you can run the entire notebook by clicking **Run All** from the menu.
