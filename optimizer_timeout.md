---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-11"

keywords: lakehouse, watsonx.data, query optimizer, timeout

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

# Updating query rewrite timeout for Query Optimizer
{: #optimizer_timeout}

The default query rewrite timeout for **Query Optimizer** is 60 seconds. You can change this value using the PATCH API after activating **Query Optimizer**.

## Procedure
{: #optimizer_timeoutprcdre}

1. Run the following PATCH API command to update the query rewrite timeout:

   ```bash
   curl --request PATCH  \
   --url https://{REGION}.lakehouse.cloud.ibm.com/lakehouse/api/v3/prestissimo_engines/{ENGINE_ID} \
   --header 'accept: application/json' \
    --header 'Content-Type: application/merge-patch+json' \
    --header 'AuthInstanceId: {CRN}' \
   --header 'Authorization: Bearer <BEARER_TOKEN>' \
   -d '{
       "display_name": "prestissimo-small",
       "description": "",
       "properties": {
           "configuration": {
               "coordinator": {
                   "query.max-history": "2000"
               },
               "worker": {
               }
           },
           "jvm": {
               "coordinator": {
               }
           },
           "catalog": {
               "hive_data": {
                   "coordinator": {
                   },
                   "worker": {}
               }
           },
           "velox": {
           },
           "log_config": {
               "coordinator": {
               },
               "worker": {}
           },
           "optimizer_properties": {
               "optplus.query-timeout-seconds":"3000"

           },
           "global": {}
       },
       "restart_type": "force",
       "tags": []
   }'
   ```
   {: codeblock}

   `<console-url>`: The watsonx.data console URL.

   `<instance-id>`: The instance identifier.

   `<engine-id>`: The Presto engine identifier.

   `<auth-instance-id>`: The authentication instance ID.

   `<token>`: The bearer token for authorization.

2. Update the value of `optplus.query-timeout-seconds` to the desired timeout in seconds.
