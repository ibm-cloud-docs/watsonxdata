---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-25"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Resource groups
{: #rg_ov}

Resource groups help to manage query execution and resource allocation. Using resource groups, administrators can control the allocation and utilization of resources on a Presto cluster. Resource groups limit resource usage and enforce policy queues on queries.
{: shortdesc}

## Key features
{: #key_feat}

- Resource groups can set limits on resource usage such as CPU time, memory usage, or total number of queries (especially in multi-tenant environments to ensure that no single user or query monopolizes the system resources).
- Resource groups do not cause query failure in complete resource consumption. Instead, new queries are queued until the resources become available again.
- Subgroups in resource groups allow hierarchical resource allocation. Each subgroup can have its own resource limits and policy queues.

For more information about resource groups, see [Resource Groups](https://prestodb.io/docs/current/admin/resource-groups.html).

For more information about Presto resource group configuration in {{site.data.keyword.lakehouse_short}}, see [Configuring Presto resource groups](watsonxdata?topic=watsonxdata-conf_rcrs_grp).

For more information about the resource group properties that you can define in the resource group JSON file, see [Resource group properties](watsonxdata?topic=watsonxdata-resource_grp_pptys).
