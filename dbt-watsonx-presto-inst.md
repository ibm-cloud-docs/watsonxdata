---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-18"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Installing and using dbt-watsonx-presto
{: #dbt_watsonx_presto_inst}

This section covers the steps to install and use `dbt-watsonx-presto`.

## Procedure
{: #dbt_watsonx_presto_inst_pros}

1. Run the following command on your system to install `dbt-watsonx-presto`.

   ```bash
   pip install dbt-watsonx-presto
   ```
   {: codeblock}

1. Run the following command to verify the dbt version.

   ```bash
   dbt –version
   ```
   {: codeblock}

1. Run the following command to create a dbt project.

   ```bash
   dbt init <project_name>
   ```
   {: codeblock}

   1. Select a Presto number and enter it. Example: for `[1] presto`, enter `1`.
   1. If you already have a project with the same name, you must confirm whether to overwrite `profiles.yml`. Enter **Y** to confirm or **N** to discard.

1. Set up the `profiles.yml` file. For more information, see [Configuration (setting up your profile)](watsonxdata?topic=watsonxdata-dbt_watsonx_presto_conf).

1. To test the connection, run:

   ```bash
   cd <project_name>
   dbt debug
   ```
   {: codeblock}

1. Create a CSV file inside the seeds folder to seed the data into {{site.data.keyword.lakehouse_short}}. For example:

   ```bash
   id, value
   1,100
   2,200
   3,300
   4,400
   ```
   {: codeblock}

   You might encounter errors when executing seed files because dbt cannot handle all the data types based on the data in the connector. To resolve this, you can explicitly define the data types that dbt should use. Go to <project_name>/dbt_project.yml and add:

   ```yaml
   seeds:
     <project_name>:
       <seed_file_name>:
         +column_types:
           <col_1>: datatype
           <col_2>: datatype
   ```
   {: codeblock}

   For example:

   ```yaml
   seeds:
     demo:
       sample:
         +column_types:
           value: VARCHAR(20)
   ```
   {: codeblock}

   Column names that are specified here should match with the columns in the CSV files.

   Do not use extra spaces in CSV files for seeding. If you include extra spaces, you must use same number of spaces while querying that in the models to avoid errors.
   {: important}

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
