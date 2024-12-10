---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-10"

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

For more information, see [API references](https://editor-next.swagger.io/?url=https://raw.githubusercontent.com/unitycatalog/unitycatalog/refs/tags/v0.1.0/api/all.yaml).

### Sample Unity APIs for GET catalogs
{: #unity_cat_api_example}

```bash
curl -k -X GET "https://80e7cce9-c14f-4aa8-8a3b-c52adc25efac.cdc406pd09pasng7elgg.lakehouse.dev.appdomain.cloud:32230/api/2.1/unity-catalog/catalogs" --header "Authorization: Bearer $token" --header 'Content-Type: application/json'

{
  "catalogs": [
    {
      "name": "ad_catalog",
      "comment": "",
      "properties": {
        "catalogType": "delta",
        "storageName": "func-test-bucket"
      },
      "created_at": 1733724384000,
      "updated_at": 0,
      "id": "3186f83a-8879-46c4-b48e-125741c34e88",
      "owner": "anurag",
      "created_by": "anurag",
      "updated_by": null
    },
    {
      "name": "testth",
      "comment": "",
      "properties": {
        "catalogType": "iceberg",
        "storageName": "mdshms"
      },
      "created_at": 1733724482000,
      "updated_at": 0,
      "id": "9ce30ab7-1321-4189-bb10-765093d1932c",
      "owner": "antony",
      "created_by": "antony",
      "updated_by": null
    }
  ],
  "next-page-token": null
}
```
{: codeblock}

### Sample Unity APIs for GET schemas for catalog
{: #unity_cat_api_example_2}

```bash
curl -k -X GET "https://80e7cce9-c14f-4aa8-8a3b-c52adc25efac.cdc406pd09pasng7elgg.lakehouse.dev.appdomain.cloud:32230/api/2.1/unity-catalog/schemas?catalog_name=mrmadira_hive_catalog" --header "Authorization: Bearer $token" --header 'Content-Type: application/json'

{
  "schemas": [
    {
      "name": "dec92024",
      "catalog_name": "mrmadira_hive_catalog",
      "comment": null,
      "properties": {
        "locationUri": "s3a://testbucket/dec92024"
      },
      "full_name": "mrmadira_hive_catalog.dec92024",
      "created_at": 0,
      "updated_at": 0,
      "schema_id": "135"
    }
  ]
}
```
{: codeblock}

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

For more information, see [API references](https://editor-next.swagger.io/?url=https://raw.githubusercontent.com/apache/iceberg/refs/tags/apache-iceberg-1.6.1/open-api/rest-catalog-open-api.yaml).

### Sample Iceberg APIs
{: #Sample_Iceberg_APIs}

#### Get namespaces for a catalog
{: #Sample_Iceberg_APIs_1}

```bash
curl -k --request GET   --url 'https://80e7cce9-c14f-4aa8-8a3b-c52adc25efac.cdc406pd09pasng7elgg.lakehouse.dev.appdomain.cloud:32230/mds/iceberg/v1/hemant_test/namespaces'   --header 'Accept: application/json'   --header "Authorization: Bearer $token"  --header 'Content-Type: application/json'  | jq

{
  "namespaces": [
    [
      "hemant_test"
    ],
    [
      "order_schema_ad"
    ],
    [
      "schema1150850f-ece4-4c27-8794-e05b984adff5"
    ]
  ],
  "next-page-token": null
}
```
{: codeblock}

#### Get tables for a schema
{: #Sample_Iceberg_APIs_2}

```bash
curl -k --request GET   --url 'https://80e7cce9-c14f-4aa8-8a3b-c52adc25efac.cdc406pd09pasng7elgg.lakehouse.dev.appdomain.cloud:32230/mds/iceberg/v1/hemant_test/namespaces/schema_cpd'   --header 'Accept: application/json'   --header "Authorization: Bearer $token"  --header 'Content-Type: application/json'  | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    74    0    74    0     0     52      0 --:--:--  0:00:01 --:--:--    52
{
  "namespace": [
    "schema_cpd"
  ],
  "properties": {
    "owner": "hemant"
  }
}
```
{: codeblock}

### Behavior and Limitations
{: #iceberg_cat_api_limit}

Due to the constraint of not modifying the schema, the following features are not supported:

- Multi-level namespace creation
- As Hive is the catalog for all databases or namespaces in the DBS table, creating namespace is not supported even if it exists in catalogs other than Iceberg.
- If you list the schema, only the namespaces for the current catalog with the specified prefix is returned. However, if you - attempt to create a namespace that exists in another catalog, a `Namespace Already Exists` exception is returned.
- When listing tables, only Iceberg tables are returned. If you attempt to create a table with a name that exists as a Hive or Delta table in the same database or namespace, the creation of an Iceberg table with the same name is not allowed.
- X-Iceberg-Access-Delegation is not supported.
- Metrics endpoint added as dummy only.
