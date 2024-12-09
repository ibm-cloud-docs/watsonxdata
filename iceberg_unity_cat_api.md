---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-09"

keywords: lakehouse, milvus, watsonx.data

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

# Unity Catalog REST API and Iceberg Catalog REST API
{: #unity_iceberg_api}

Metadata Service implements selected APIs from the Iceberg REST Catalog and Unity Catalog Open API spec. You can leverage these APIs from standard REST Clients. Use of REST Client has the benefit of directly interacting with the metastore without an engine.
{: shortdesc}

## Unity Catalog REST API
{: #unity_cat_api}

The following are the APIs included:

### Catalogs
{: #unity_cat_api_1}

- POST /catalogs
- GET /catalogs
- GET /catalogs/{name}
- PATCH /catalog/{name}
- DELETE /catalog/{name}

### Schemas
{: #unity_cat_api_2}

- POST /schemas
- GET /schemas
- GET /schemas/{full_name}
- PATCH /schemas/{full_name}
- DELETE /schemas/{full_name}

### Tables
{: #unity_cat_api_3}

- POST /tables
- GET /tables
- GET /tables/{full_name}
- DELETE /tables/{full_name}

### Behavior and limitations
{: #unity_cat_api_limit}

Due to the constraint of not modifying the schema, some required fields must be included in the `properties` field of the Unity REST spec.

For creating a catalog, the `locationUri`, bucket name (registered with watsonx.data), and `catalogType` fields are mandatory and must be provided in the `properties` field:

```bash
"properties": {
    "locationUri": "s3a://func-test-bucket/unity_schema",
    "bucket": "func-test-bucket",
    "catalogType": "ICEBERG"
}
```
{: codeblock}

For creating schemas, the locationUri is a required field and must be included in the `properties` field:

```bash
"properties": {
    "locationUri": "s3a://func-test-bucket/unity_schema"
}
```
{: codeblock}

For creating tables, there are additional fields in the Unity spec that are not available. Metadata Service ignores any information that is provided for these fields and is not stored in the database:

```bash
"columns": [
    {
      "type_json": "string",
      "type_name": "string",
      "type_precision": 0,
      "type_scale": 0,
      "type_interval_type": "string",
      "position": 0,
      "nullable": true,
      "partition_index": 0
    }
]
```
{: codeblock}

If extra values are passed in the properties of request object, they are not stored in any table due to adherence to the current HMS schema. You can include additional details in the `properties` field in future if needed.
{: note}

## Iceberg Catalog REST API
{: #iceberg_cat_api}

The following are the APIs included:

### Namespaces
{: #iceberg_cat_api_1}

- List namespaces
- Create a namespace
- Load metadata properties for namespace
- Check whether namespace exists
- Drop namespace

### Iceberg table related
{: #iceberg_cat_api_2}

- Create a table in the given namespace
- Register a table by using metadata_location
- Load a table
- Check whether a table exists
- Rename a table
- Commit updates to multiple tables in an atomic transaction
- Commit updates to a table
- Drop table

### Views
{: #iceberg_cat_api_3}

- List all view identifiers
- Load a view
- Check whether a view exists
- Rename a view
- Drop view

### Config
{: #iceberg_cat_api_4}

- Config endpoint to configure catalog as prefix

## Behavior and Limitations
{: #iceberg_cat_api_limit}

Due to the constraint of not modifying the schema, the following features are not supported:

- Multi-level namespace creation
- As Hive is the catalog for all databases or namespaces in the DBS table, creating namespace is not supported even if it exists in catalogs other than Iceberg.
- If you list the schema, only the namespaces for the current catalog with the specified prefix is returned. However, if you - attempt to create a namespace that exists in another catalog, a `Namespace Already Exists` exception is returned.
- When listing tables, only Iceberg tables are returned. If you attempt to create a table with a name that exists as a Hive or Delta table in the same database or namespace, the creation of an Iceberg table with the same name is not allowed.
