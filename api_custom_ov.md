---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-20"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# API customization
{: #api_custom_ov}

API customization in {{site.data.keyword.lakehouse_short}} provides a way for instance administrators to customize JVM, CONFIG, catalog, and Velox (Presto (C++)) properties for Presto (Java) and Presto (C++) engines through an API.

This customization method does not require you to add the parameters inside the pod, restart the pod (if there is CPD deployment), or reach out to support personnel (if there is SaaS deployment) for customization. It also does not require any special access and privileges to the backend system. API customization is a unified way to customize allowed properties in {{site.data.keyword.lakehouse_short}}, regardless of the deployment. API customization is supported through the PATCH API. API endpoints and sample requests for Presto (Java) and Presto (C++) engines are as follows:

## PATCH API (Presto (Java) engine)
{: #api_pjava}

### Endpoint
{: #api_pjava_ep}

```bash
/presto_engines/{engine_id}
```
{: codeblock}

### Request body
{: #api_pjava_rb}

```json
{
  "description": "updated description for presto engine",
  "engine_display_name": "sampleEngine",
  "engine_properties": {
    "configuration": {
      "coordinator": {
        "property_1": "property_value",
         "property_2": "property_value"
      },
      "worker": {
        "property_1": "property_value",
         "property_2": "property_value"
      }
    },
    "jvm": {
      "coordinator": {
        "property_1": "property_value",
         "property_2": "property_value"
      },
      "worker": {
        "property_1": "property_value",
         "property_2": "property_value"
      }
    },
   "catalog":{
      "catalog_name":{
           "property_1": "property_value",
         "property_2": "property_value"
      },
},
"global":{

}
   },
  "engine_restart": "force",
  "remove_engine_properties": {
    "configuration": {
      "coordinator": [
        "property1","property2"
      ],
      "worker": [
         "property1","property2"
      ]
    },
    "jvm": {
      "coordinator": [
         "property1","property2"
      ],
      "worker": [
         "property1","property2"
      ]
    },
  "catalog":{
"catalog_name":["property1","property2"]
  },
"global":{

}
  },
  "tags": [
    "tag1",
    "tag2"
  ]
}
```
{: codeblock}

## PATCH API (Presto (C++) engine)
{: #api_pcpp}

### Endpoint
{: #api_pcpp_ep}

```bash
/prestissimo_engines/{engine_id}
```
{: codeblock}

### Request body
{: #api_pcpp_rb}

```json
{
  "description": "updated description for prestissimo engine",
  "engine_display_name": "sampleEngine",
  "engine_properties": {
    "configuration": {
      "coordinator": {
        "property_1": "property_value",
         "property_2": "property_value"
      },
      "worker": {
        "property_1": "property_value",
         "property_2": "property_value"
      }
    },
   "catalog":{
      "catalog_name":{
           "property_1": "property_value",
         "property_2": "property_value"
      }},
    "velox": {
			"property_1": "property_value",
         "property_2": "property_value"
		}
  }
   },
  "engine_restart": "force",
  "remove_engine_properties": {
    "configuration": {
      "coordinator": [
        "property1","property2"
      ],
      "worker": [
         "property1","property2"
      ]
    },
  "catalog":{
"catalog_name":["property1","property2"]
  },
"velox":
[
  "property1","property2"
      ]

  },
  "tags": [
    "tag1",
    "tag2"
  ]
}
```
{: codeblock}

The GET API also supports customization, but is available for internal use only.
{: note}

You can find the curl example for API customization in [Update presto engine](https://cloud.ibm.com/apidocs/watsonxdata#update-presto-engine).

For the list of properties that can be customized through an API for Presto (Java), see:

- [Configuration properties for Presto (Java) - coordinator and worker nodes](watsonxdata?topic=watsonxdata-api_custom_prm_pjcw)
- [JVM properties for Presto (Java) - Coordinator and worker nodes](watsonxdata?topic=watsonxdata-api_custom_jvm_pjcw)
- [Catalog properties for Presto (Java)](watsonxdata?topic=watsonxdata-api_custom_ctg_pjcw)

For the list of properties that can be customized through an API for Presto (C++), see:

- [Configuration properties for Presto (C++) - worker nodes](watsonxdata?topic=watsonxdata-api_custom_wkr_pcpp)
- [Configuration properties for Presto (C++) - coordinator nodes](watsonxdata?topic=watsonxdata-aapi_custom_pcpp_cood)
- [Catalog properties for Presto (C++)](watsonxdata?topic=watsonxdata-api_custom_pcpp_ctg)
- [Velox properties for Presto (C++)](watsonxdata?topic=watsonxdata-api_custom_pcpp_vlx)

For properties that must be customized under the guidance of the watsonx.data support team, see [Properties to be customized under support guidance](watsonxdata?topic=watsonxdata-api_custom_wkr_pcpp#api_custom_sprt_pcpp).


