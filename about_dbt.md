---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-15"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Data Build Tool (dbt) integration
{: #abt_dbt}

{{site.data.keyword.lakehouse_full}} integrates with Data Build Tool (dbt), which is a data analytics tool that helps to transform the data in {{site.data.keyword.lakehouse_short}} to simpler and accessible form for business users. It allows analysts and scientists to build data pipelines by using different models and have curated data for decision making. You can run SQL queries by using the db tool and analyse data available in {{site.data.keyword.lakehouse_short}}.

dbt allows analysts and scientists with some of the following data related tasks:

   * Manage complex work flows for data transformation and support features like version control, modular code, and continuous integration.

   * Prepare data for reporting and analysis by transforming raw data into a structured format, making it easier to create insights.

   * Create layered, reusable models that represent different stages of data transformation.

   * Ensure reliability of the transformations by identifying issues in the process.

   * Generate clear and easy-to-understand documentation for the models and provide visualization of data lineage to track how data moves through the pipeline.

   * Handle dependencies between models and ensure the transformations run in the correct sequence and can integrate with larger data workflow.

For more information about dbt, see:

- [What is dbt?](https://docs.getdbt.com/docs/introduction)
- [About dbt projects](https://docs.getdbt.com/docs/build/projects)

dbt is supported in {{site.data.keyword.lakehouse_short}} for Spark and Presto engines. dbt uses the following data build tool (dbt) adapters to connect dbt core with Spark and Presto engines. The adapters helps to build, test, and document data models.


   * dbt-watsonx-presto to connect to Presto
   * dbt-watsonx-spark to connect to Apache Spark



## Basic dbt commands
{: #dbt_watsonx_spk_cmd}

- **Initialize a dbt project**: Set up a new dbt project.

   ```bash
   dbt init my_project
   ```
   {: codeblock}

- **Debug dbt connection**: Test your dbt profile and connection.

   ```bash
   dbt debug
   ```
   {: codeblock}

- **Seed data**: Load seed data into your database/datasource.

   ```bash
   dbt seed
   ```
   {: codeblock}

- **Run dbt models**: Build and run your models.

   ```bash
   dbt run
   ```
   {: codeblock}

- **Test dbt models**: Run tests on your models.

   ```bash
   dbt test
   ```
   {: codeblock}

- **Generate documentation**: Create and serve documentation for your dbt project.

   ```bash
   dbt docs generate
   dbt docs serve
   ```
   {: codeblock}

For more information about dbt commands, see [dbt command reference](https://docs.getdbt.com/reference/dbt-commands).
