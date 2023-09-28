---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-27"

keywords: high availability, disaster revecory, watsonx.data

subcollection: watsonxdata

---

<!--{:javascript: #javascript .ph data-hd-programlang='javascript'}
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
{:video: .video} -->

{{site.data.keyword.attribute-definition-list}}


# High availability and disaster recovery
{: #hadr_wxd}

{{site.data.keyword.lakehouse_full}} service instances are deployed in IBM Cloud multi-zone region (MZR) and AWS MZR . The availability of {{site.data.keyword.lakehouse_short}} components is Active-Active and Active-Only.
{: shortdesc}

## Active-Active
{: #Act-Act}

Multi-tenant components support multiple customers and are configured with multiple replicas across Availability Zones (AZs) to ensure availability. This category consists of most of the {{site.data.keyword.lakehouse_short}} components.

## Active-Only
{: #Act-Oly}

Single-tenant components in this category are dedicated to a single customer. This category consists of the Presto engine and metastore. These components restart in a new zone if there is a failure.

**In Multi Zone Regions (MZRs), Presto and HMS are distributed across different zones.**

When a single availability zone fails in an MZR, or a hardware failure occurs in any region, the workloads automatically fail and restart in other zones within that region. Every {{site.data.keyword.lakehouse_short}} instance comes with a default cross-regional Metadata bucket and an optional Trial bucket(10 GB). Both the buckets are enabled with IBM Cloud® Object Storage Versioning. The data is backed up by enabling replication to a separate IBM Cloud Object Storage Account. However, for any external bucket that the customer brings into {{site.data.keyword.lakehouse_short}} instance, the customer is responsible for those backups.

In case of a regional disaster, you will receive an email that includes all the steps that you need to follow. See responsibilities for {{site.data.keyword.lakehouse_short}}.
Single-tenant components operate on an 'Active Only' model, ensuring immediate restart on new nodes that provide the same service if there is a failure.

Single-tenant components are strategically distributed across 3 AZs to enhance reliability. When an AZ fails, sufficient capacity to initiate the required services on the available AZs is ensured. This minimizes any impact that is caused by an AZ outage.


## Responsibilities
{: #resplty}

| Task  |IBM Responsibilities |Your Responsibilities|
|---|---|---|
| Backups |{{site.data.keyword.lakehouse_short}} is responsible for automatic daily backups, of all {{site.data.keyword.lakehouse_short}} provided resources. |**The Client is responsible for:** **1)** Create a new instance of IBM {{site.data.keyword.lakehouse_short}} to restore the backups and validate that the IBM backups that are restored properly. **2)** Restore backups of external components that they brought into {{site.data.keyword.lakehouse_short}}.
|  Restore |{{site.data.keyword.lakehouse_short}} handles the restoration of backups for provided resources.   |**The Client is responsible for:** **1)** Create a new instance of {{site.data.keyword.lakehouse_short}} to restore the backups and validate that the IBM backups that are restored properly. **2)** Restore backups of external components that they brought into {{site.data.keyword.lakehouse_short}}.|
{: caption="Table 1. Responsibilities" caption-side="bottom"}

## Application-level high availability
{: #appl-ha}

Applications that communicate over networks and cloud services are subject to transient connection failures. Design your applications to retry connections when a temporary loss in connectivity to your deployment or to IBM Cloud, causes errors. As {{site.data.keyword.lakehouse_short}} is a managed service, regular updates and maintenance occur as part of normal operations. Such maintenance occasionally causes a temporary service interruption.

Your applications must be designed to handle temporary interruptions to the service, implement error handling for failed commands, and implement retry logic to recover from a temporary interruption.

**Following are some of the error codes that might be expected during the temporary service interruptions:**

If a Presto coordinator node restarts, be it for maintenance purposes or due to a system failure, applications are required to reestablish their connection with the Presto engine.

Several minutes of unavailability or connection interruptions are not expected. Open a support ticket with details if you have time periods longer than a minute with no connectivity so that the interruptions are investigated.

## Disaster Recovery Strategy
{: #diastr_rec_str}

{{site.data.keyword.lakehouse_full}} provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted recovery point objective (RPO) and recovery time objective (RTO) for the service. The following table outlines the targets for {{site.data.keyword.lakehouse_short}}.

| Disaster recovery objective   | Target Value |
|-------------------------------|:------------:|
| RPO                           |  <= 24 hours |
| RTO                           |  < 24 hours  |
{: caption="Table 2. Disaster Recovery Strategy" caption-side="bottom"}

## Locations
{: #locations}

### AWS Regions
{: #aws_regns}

1. Oregon (us-west-2)
2. N. Virginia (us-east-1)
3. Frankfurt (eu-central-1)

### IBM Regions
{: #ibm_regns}

1. Dallas (us-south)
2. Washington (us-east)
