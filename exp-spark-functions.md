---

copyright:
  years: 2017, 2023
lastupdated: "2023-10-11"

keywords: watsonx.data, spark, table, maintenance,
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Exploring {{site.data.keyword.iae_short}} integration capabilities
{: #exp_cap}

The functions achievable through the {{site.data.keyword.iae_full_notm}} integration include:
* [Accessing tables from {{site.data.keyword.lakehouse_short}}](#exp_access)
* [Ingesting data to {{site.data.keyword.lakehouse_short}}](#exp_ingest)
* [Modifying schema in {{site.data.keyword.lakehouse_short}}](#exp_modify)

## Prerequisites
{: #exp_preq}

<!-- Inputs required -->



## Customizing the sample file
{: #exp_cust}

You can customize the [sample python file](#python_file) with desired values. Change the paarmeter values in each code snippet to get customized results.

### Accessing tables from {{site.data.keyword.lakehouse_short}}
{: #exp_access}

The following snippet displays a section from the [sample python file](#python_file) which allows you to create new tables inside {{site.data.keyword.lakehouse_short}}. You can customize by providing the desired parameter values.

   ```bash
        # Create a database in lakehouse catalog
        spark.sql("create database if not exists lakehouse.DATABASE_NAME LOCATION 's3a://lakehouse-bucket/'")
        # list the database under lakehouse catalog
        spark.sql("show databases from lakehouse").show()

        # demonstration#1: Create a basic Iceberg table, insert some data and then query table
        spark.sql("create table if not exists lakehouse.DATABASE_NAME.TABLE_NAME(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
        spark.sql("insert into lakehouse.DATABASE_NAME.TABLE_NAME values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
        spark.sql("select * from lakehouse.DATABASE_NAME.TABLE_NAME").show()
   ```
   {: codeblock}

    Parameter values:
    * DATABASE_NAME: Specify the name of the database that needs to be created inside the catalog.
    * TABLE_NAME: The iceberg table that needs to be created inside the database.


### Ingesting data to {{site.data.keyword.lakehouse_short}}
{: #exp_ingest}

The following snippet displays a section from the [sample python file](#python_file) which allows you to ingest data into tables inside {{site.data.keyword.lakehouse_short}}. You can ingest data in parquet and CSV formats. You can customize by providing the desired parameter values.

### Ingesting data in parquet format
{: #exp_parquet}

   ```bash
        # demonstration#2: Ingest parquet data into a lakehouse table
        # load parquet data into dataframce
        df = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-01.parquet")
        # write the data frame into an Iceberg table
        df.writeTo("lakehouse.DATABASE_NAME.DATA_COLUMN").create()
        # describe the table created
        spark.sql('describe table lakehouse.DATABASE_NAME.DATA_COLUMN').show(25)
        # query the table
        spark.sql('select * from lakehouse.DATABASE_NAME.DATA_COLUMN').count()
   ```
   {: codeblock}

    Parameter values:
    * DATA_COLUMN: Specify the name of the column.
    * TABLE_NAME: The iceberg table that needs to be created inside the database.

### Ingesting data in CSV format
{: #exp_csv}

## Modifying schema in {{site.data.keyword.lakehouse_short}}
{: #exp_modify}

The following snippet displays a section from the [sample python file](#python_file) which allows you to modify data in {{site.data.keyword.lakehouse_short}}. You can customize by providing the desired parameter values.

   ```bash
        # demonstration#3: Schema evolution
        # Add column fare_per_mile to the table
        spark.sql('ALTER TABLE lakehouse.DATABASE_NAME.DATA_COLUMN ADD COLUMN(fare_per_mile double)')
        # describe the table
        spark.sql('describe table lakehouse.demoDB.DATA_COLUMN').show(25)
        # compute value for the newly added column fare_per_mile
        spark.sql('update lakehouse.DATABASE_NAME.DATA_COLUMN set fare_per_mile = total_amount/trip_distance')
        spark.sql('select * from lakehouse.DATABASE_NAME.DATA_COLUMN').show()
   ```
   {: codeblock}
