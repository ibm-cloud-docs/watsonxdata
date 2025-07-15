---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-15"

keywords: lakehouse, watsonx.data, spark, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Installing and using dbt-watsonx-spark
{: #dbt_watsonx_spark_inst}

This section covers the steps to install and use `dbt-watsonx-spark`.

## Before you begin
{: #bfb_dbt}

* Subscription to watsonx.data on IBM Cloud.
* Provision native Spark engine in watsonx.data.
* Install [DBT core](https://pypi.org/project/dbt-watsonx-spark/).

## Procedure
{: #dbt_watsonx_spark_inst_pros}



### Create a Spark query server
{: #dbt_watsonx_spark_inst_1}

For the Spark engine to integrate with dbt tool and work as a query engine, you must create a Spark query server. See [Create a Spark query server](/docs/watsonxdata?topic=watsonxdata-spk_qry_srver#crt_spk_qry_srver).



### Retrieve the query server connection details
{: #dbt_watsonx_spark_inst_2}


To configure the profile file in dbt tool, you must save the query server connection details. See [Retrieve the query server connection details](/docs/watsonxdata?topic=watsonxdata-spk_qry_srver#ret_con_dtls).



### Set up profiles.yaml for dbt tool
{: #dbt_watsonx_spark_inst_3}

1. Go to the `profiles.yml` file that is located in .dbt of your home directory.
1. Paste the connection details by modifying the parameter values.
1. Set up the `profiles.yml` file. For more information, see Configuration (setting up your profile).


### Install the dbt tool and verify the connection
{: #dbt_watsonx_spark_inst_4}


1. Run the following command on your system to install `dbt-watsonx-spark`.

   ```bash
   pip install dbt-watsonx-spark
   ```
   {: codeblock}

1. Run the following command to verify the dbt version.

   ```bash
   dbt --version
   ```
   {: codeblock}

1. If you want to create a dbt project, provide a <project_name> and run the following command .

   ```bash
   dbt init <project_name>
   ```
   {: codeblock}

    1. The system prompts to select the database to be used. Select `watsonx_spark`.
    1. Provide watsonx.data host, URI, and schema.

1. To test the connection, run:

   ```bash
   cd <project_name>
   dbt debug
   ```
   {: codeblock}

1. Run the seeds by using the following command to create a table and insert the data.

   ```bash
   cd <project_name>
   dbt run
   ```
   {: codeblock}

1. In `<project_name>/models`, you have the models that perform the operations. By default, dbt sets the operations as `view`. You can create the tables or views by one of the following methods:

   - **Specify inside the models (applicable for that model only)**

     ```bash
     {{ config(materialized='table/view') }}
     ```
     {: codeblock}

     If this statement is commented out using (--), dbt still uses the configuration. To disable it, remove it entirely or comment it in Jinja style (`{# … #}`).
     {: note}

   - **Specify in dbt_project.yml (applicable for all models)**

     ```yaml
     models:
       <project_name>:
         <model_folders>:
           +materialized: table/view
     ```
     {: codeblock}

     For example:

     ```yaml
     models:
       demo:
         example:
           +materialized: table
     ```
     {: codeblock}

     Only select statements are supported within models.
     {: note}

   The semicolon (;) character is restricted in models.
   {: important}

1. Run the models by using the following command to create the tables or views.

   ```bash
   cd <project_name>
   dbt run
   ```
   {: codeblock}

   You can also specify the tests that you want:

   ```yaml
   models:
     - name: <model_name>
       description: "some description"
       columns:
         - name: <col_name>
           description: "some description"
           data_tests:
             - <test_name_1>
             - <test_name_2>
   ```
   {: codeblock}

   For example:

   ```yaml
   models:
     - name: my_first_dbt_model
       description: "A starter dbt model"
       columns:
         - name: id
           description: "The primary key for this table"
           data_tests:
             - unique
             - not_null
   ```
   {: codeblock}

   Connectors must support Create Table as Select (CTAS) for dbt runs to work.
   {: important}

1. To generate the documents about the actions performed, run:

   ```bash
   cd <project_name>
   dbt docs generate
   dbt docs serve
   ```
   {: codeblock}

    By default, it runs on localhost:8080. To change the port, run:

    ```bash
    dbt docs serve –-port <port_number>
    ```
    {: codeblock}
