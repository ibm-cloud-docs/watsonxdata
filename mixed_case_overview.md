---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-11"

keywords: lakehouse, mixed-case, watsonx.data

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

# Presto (Java) mixed-case support overview
{: #mixed_case_overview}

Case-sensitivity refers to the Presto (Java) engine’s capability to distinguish between uppercase and lowercase letters, treating them as distinct characters. This is important when querying databases, as the case of table and column names can affect the query results.
{: shortdesc}

## Case-insensitive behavior
{: #case-insensitive_behavior}

Presto (Java) engine behavior in {{site.data.keyword.lakehouse_full}} was case-insensitive till version 1.0.3. Case sensitivity was introduced in version 1.1.0. All Presto (Java) engine versions from 1.1.0 and above are case-sensitive by default. The table names in the following examples are stored and fetched separately.

1. SELECT * FROM catalog1.schema1.table;
2. SELECT * FROM catalog1.schema1.TABLE;
3. SELECT * FROM catalog1.schema1.TaBle;

## Case-sensitive behavior
{: #case-sensitive_behavior}

Presto (Java) engine behavior in {{site.data.keyword.lakehouse_full}} was case-insensitive till version 1.0.3. Case sensitivity was introduced in version 1.1.0. All Presto (Java) engine versions from 1.1.0 and above are case-sensitive by default. The table names in the following examples are stored and fetched separately.

1. SELECT * FROM catalog1.schema1.table;
2. SELECT * FROM catalog1.schema1.TABLE;
3. SELECT * FROM catalog1.schema1.TaBle;

## Mixed-case feature flag
{: #mixed_case_flag}

From {{site.data.keyword.lakehouse_full}} version 2.0.0, a new feature is available to switch between both case-sensitive and case-insensitive behavior in Presto (Java) by using a mixed-case feature flag. The mixed-case feature flag is set to OFF in Presto (Java) by default. The flag can be set to ON or OFF as required during deployment of the Presto (Java) engine. It is advised not to toggle between ON and OFF configurations after the deployment, as it may result in inconsistent system behavior.

To configure the flag, you can either configure it by using the [Customization API](https://cloud.ibm.com/apidocs/watsonxdata-software#update-presto-engine){: external} or reach out to the support team.

You can use the following curl command to set the flag as true or false:

   ```bash
   {
	"description": "updated description for presto engine",
	"engine_display_name": "<engine_display_name>",
	"engine_properties": {
		"configuration": {
			"coordinator": {
			},
			"worker": {
			}
		},
		"jvm": {
			"coordinator": {
			},
			"worker": {
			}
		},
		"catalog": {
			"<catalog_name>": {
				"coordinator": {
				},
				"worker": {
				}
			}
		},
		"event_listener": {
		},
		"jmx_exporter_config": {
		},
		"log_config": {
			"coordinator": {
			},
			"worker": {
			}
		},
		"global": {
		}
	},
	"engine_restart": "force",
	"remove_engine_properties": {
		"configuration": {
			"coordinator": [
			],
			"worker": [
			]
		},
		"jvm": {
			"coordinator": [
			],
			"worker": [
			]
		},
		"log_config": {
			"coordinator": [
			],
			"worker": [
			]
		},
		"event_listener": [
		],
		"global": [
		],
		"jmx_exporter_config": [
		],
		"catalog": {
		}
	},
	"tags": [
	]
}
   ```
   {: codeblock}

The following are the two scenarios to illustrate mixed-case support behavior:

## Scenario 1: Mixed-case feature flag ON
{: #mixed_case_flagon}

A. Create multiple tables in the mixed-case feature flag ON cluster for both lowercase and mixed case table names.
* The user can access all the tables.

B. Change the setting for mixed-case feature flag from ON to OFF.
* If there are multiple tables with same name but in mixed cases, then such tables may not be accessible or can cause data discrepancy depending on the connector used.

## Scenario 1: Mixed-case feature flag OFF
{: #mixed_case_flagoff}

A. Create multiple tables in the mixed-case feature flag OFF cluster.
* For duplicate table names, only the table that is created first will be fetched.
* For unique table names, all tables are created and fetched.

B. Change the setting for mixed-case feature flag from OFF to ON.
* The user can access all the tables.

For more information on mixed-case behavior, see [Mixed-case behavior based on connectors](watsonxdata?topic=watsonxdata-mixed_case_behavior){: external}.
