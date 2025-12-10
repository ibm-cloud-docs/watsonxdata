---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-01"

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
   curl --request PATCH \
     --url https://console-aws-usgoveast1.watsonxdata.prep.ibmforusgov.com/lakehouse/api/v3/20250819-0756-4270-23ea-c33f4aeffbbf/prestissimo_engines/prismo197 \
     --header 'Authinstanceid: crn:v1:awsgov-staging:public:lakehouse:us-gov-east-1:sub/20250625-1243-0601-03a6-6951b59f6780:20250819-0756-4270-23ea-c33f4aeffbbf::' \
     --header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.   eyJpc3MiOiJJQk1MSCIsInN1YiI6IlNlcnZpY2VJZC0xZmIzNWY3My05ZmY2LTQwMGQtODc1Ni02ZGZjZjNkZDdhZGQiLCJhdWQiOlsiQU1TIl0sImV4cCI6MTc1NzMxODczOCwiaWF0IjoxNzU3MzE3NTM4LCJ1a   WQiOiIxZmIzNWY3My05ZmY2LTQwMGQtODc1Ni02ZGZjZjNkZDdhZGQiLCJwZXJtaXNzaW9ucyI6bnVsbCwiZ3JvdXBzIjpbXSwiaW5zdGFuY2UiOnsidXNlcm5hbWUiOiJTZXJ2aWNlSWQtMWZiMzVmNzMtOWZmNi   00MDBkLTg3NTYtNmRmY2YzZGQ3YWRkIiwiaW5zdGFuY2VfbmFtZSI6IiIsImluc3RhbmNlX2lkIjoiY3JuOnYxOmF3c2dvdi1zdGFnaW5nOnB1YmxpYzpsYWtlaG91c2U6dXMtZ292LWVhc3QtMTpzdWIvMjAyNTA   2MjUtMTI0My0wNjAxLTAzYTYtNjk1MWI1OWY2NzgwOjIwMjUwODE5LTA3NTYtNDI3MC0yM2VhLWMzM2Y0YWVmZmJiZjo6Iiwicm9sZXMiOlsiU2VydmljZUFkbWluIiwiU2VydmljZVVzZXIiXX0sInVzZXJuYW1l   IjoiU2VydmljZUlkLTFmYjM1ZjczLTlmZjYtNDAwZC04NzU2LTZkZmNmM2RkN2FkZCIsImRpc3BsYXlfbmFtZSI6InBlcmYtd3hkIiwiY2VydF9zZXJpYWxfbnVtYmVyIjoiNDg2MTQ0MTUyNjkwNTUyMzg2NDY1M   TMzNzczMDY4NjY3NTc5NzEyMTMzIiwiYnNzX2FjY291bnRfaWQiOiIifQ.   H4lX4uGPezoTi2Xfinm8gYoIQMw2eaA6e1WyFXK843fVC3NAi1e4N9By30eLogaXUWnPp85vIYGYzfpKOYaPCag8vbHym1OjdUMstFmfn4y6tsrPnTFGMGjxZKjINl50pitcF76SSRh2GHT9wf09EatSZTWRia8yr   ORI5CJCyDrxVcTVwKwiE3ImUepsFCKg5VOJxV1ARI513T2mvvDP2aiOjr9w7xIXzBl2hNfLahv__CqnmvEpsZsSD-4IC1xDvtC6OH157IBf_3ZUwsW_PobRLzoSTi7V0tDol_G5cel8cjsxYI8PeZzay97tjuSnRd   4t_-04sEciil_nMvjibw' \
     --header 'content-type: application/json' \
     --data '{
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
   			"optplus.query-timeout-seconds":"2000"

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
