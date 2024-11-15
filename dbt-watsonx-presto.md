---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-06"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# dbt-watsonx-presto (data build tool adapter for Presto)
{: #dbt_watsonx_presto}

`dbt-watsonx-presto` is a data build tool (dbt) adapter that is designed to connect dbt Core with Presto. This adapter helps to build, test, and document data models in Presto.

For more information about dbt, see:

- [What is dbt?](https://docs.getdbt.com/docs/introduction)
- [About dbt projects](https://docs.getdbt.com/docs/build/projects)

The data types that are supported by the `dbt-watsonx-presto` adapter are:

- INT
- VARCHAR
- BOOLEAN
- DATE

For information about setting up your profile, see [Configuration (setting up your profile)]({{site.data.keyword.ref-dbt_watsonx_presto_conf-link}}).

For information about installing and using `dbt-watsonx-presto`, see [Installing and using dbt-watsonx-presto]({{site.data.keyword.ref-dbt_watsonx_presto_inst-link}}).

## Limitations
{: #dbt_watsonx_presto_limit}

- The following features of dbt are not supported on Presto:
   - Archival
   - Incremental models
- The Presto and connector-related limitations are applicable to dbt also.

## Basic dbt commands
{: #dbt_watsonx_presto_cmd}

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
