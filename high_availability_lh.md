---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-23"

keywords: high availability, disaster revecory, watsonx.data

subcollection: watsonxdata

---



{{site.data.keyword.attribute-definition-list}}


# High availability and disaster recovery
{: #hadr_wxd}

High Availability (HA) and Disaster Recovery (DR) in {{site.data.keyword.lakehouse_full}} on IBM Cloud are designed to help ensure resilience, minimal downtime, and data protection.
{: shortdesc}



## High Availability (HA)
{: #high-avail}

{{site.data.keyword.lakehouse_full}} uses Multi-Zone Regions (MZRs) on both IBM Cloud and AWS to provide high availability. The various components of {{site.data.keyword.lakehouse_short}} are deployed in Active-Active and Active-Only setup to help ensure high availability and resilience.

## Active-Active
{: #Act-Act}

In an Active-Active setup, multiple instances of a component are running simultaneously across different Availability Zones (AZs). These instances are load balanced and can handle requests in parallel.

**Key characteristics**:

* Redundancy - If one instance or AZ fails, others continue to serve traffic without interruption.
* Load distribution - Traffic is distributed across all active instances, improving performance and reducing latency.
* Automatic failover - No manual intervention is needed; the system reroutes traffic automatically.

**Benefits**:

* High fault tolerance.
* Seamless user experience during zone failures.
* Better resource usage.

In {{site.data.keyword.lakehouse_short}} most of the components are deployed in Active-Active setup with replicas in multiple zones to help ensure continuous availability. For example, Metadata Services (MDS) in the Enterprise plan.



## Active-Only
{: #Act-Oly}

In an Active-Only setup, a component runs in only one Availability Zone at a time. If that zone fails, the component must be restarted or redeployed in another zone.

**Key characteristics**:

* Single active instance per component.
* Automatic restart in a new zone upon failure.
* Slight delay during failover due to restart time.

**Benefits**:

* Simpler architecture.
* Reduced resource consumption.
* Resilience with a brief downtime during failover.

In {{site.data.keyword.lakehouse_short}}, single-tenant components are deployed in Active-Only setup. These single-tenant components, which include Presto engine and metastore components, are strategically distributed across three AZs for capacity and failover. These components restart in a new zone during failure. For example, Metadata Services (MDS) in the Lite plan.



**In Multi-Zone Regions (MZRs), Presto and MDS are distributed across different zones.**

When a single availability zone fails in an MZR, or a hardware failure occurs in any region, the workloads automatically fail and restart in other zones within that region. Every {{site.data.keyword.lakehouse_short}} instance comes with a default cross-regional Metadata bucket and an optional Trial bucket(10 GB). Both the buckets are enabled with IBM Cloud® Object Storage Versioning. The data is backed up by enabling replication to a separate IBM Cloud Object Storage Account. However, for any external bucket that the customer brings into {{site.data.keyword.lakehouse_short}} instance, the customer is responsible for those backups.

In a regional disaster, you receive an email that includes all the steps that you need to follow. See responsibilities for {{site.data.keyword.lakehouse_short}}.
Single-tenant components operate on an 'Active Only' model, ensuring immediate restart on new nodes that provide the same service if there is a failure.

Single-tenant components are strategically distributed across 3 AZs to enhance reliability. When an AZ fails, sufficient capacity to initiate the required services on the available AZs is ensured. This minimizes any impact that is caused by an AZ outage.



## Responsibilities
{: #resplty}

### Backup
{: #backup}

**IBM responsibilities**
* Automatic daily backups: {{site.data.keyword.lakehouse_short}} automatically performs daily backups of all resources that are provided and managed by IBM. This includes:
   * System metadata
   * Configuration settings
   * Internal data managed by watsonx.data
* Backup storage and security: These backups are stored securely within IBM’s infrastructure, ensuring data durability and compliance with enterprise-grade standards.

**Client responsibilities**
1. Provision a new instance for restore:
   * If a restore is needed, the client must create a new watsonx.data instance to receive the restored data.
   * This ensures that the original environment remains untouched and the restored data can be validated safely.
2. Validate IBM backups:
   After restoration, the client must verify the integrity and completeness of the restored data. This includes checking metadata, configurations, and system behavior.
3. Restore external components:
   * Any external data sources or components integrated into {{site.data.keyword.lakehouse_short}} (for example, custom connectors, third-party tools, user-managed datasets) are not backed up by IBM.
   * The client is responsible for backing up and restoring these components separately.

### Restore
{: #restore}

**IBM responsibilities**

Restoration of provided resources:
IBM handles the actual restoration process for the resources it backs up. This includes loading the backup into the new instance and ensuring system-level consistency.

**Client responsibilities**
1. Create a new instance for restore:
   The client must initiate a new {{site.data.keyword.lakehouse_short}} instance to receive the restored data.
2. Validate restored data:
   The client must perform post-restore validation to ensure the restored data is accurate and usable.
3. Restore external components:
   The client must manually restore any external integrations or data sources that were part of the original setup.

## Application-level high availability
{: #appl-ha}

Applications that communicate over networks and cloud services are subject to transient connection failures. Design your applications to retry connections when a temporary loss in connectivity to your deployment or to IBM Cloud, causes errors. As {{site.data.keyword.lakehouse_short}} is a managed service, regular updates and maintenance occur as part of normal operations. Such maintenance occasionally causes a temporary service interruption.

Your applications must be designed to handle temporary interruptions to the service, implement error handling for failed commands, and implement retry logic to recover from a temporary interruption.

**The following are some of the error codes that might be expected during the temporary service interruptions:**

If a Presto coordinator node restarts, be it for maintenance purposes or due to a system failure, applications are required to reestablish their connection with the Presto engine.

Several minutes of unavailability or connection interruptions are not expected. Open a support ticket with details if you have time periods longer than a minute with no connectivity so that the interruptions are investigated.

## Disaster Recovery Strategy
{: #diastr_rec_str}

Recovery Time Objective (RTO) refers to the maximum acceptable duration of time that a system or service can be unavailable after a failure. It defines how quickly the system must be restored to avoid significant disruption to operations. RTO in watsonx.data depends on the following aspects:

* The most recent backup point.
* Log archiving status.
* Manual steps required for metadata restoration.

Recovery Point Objective (RPO) refers to the maximum acceptable amount of data loss in the event of a failure. It indicates how far back in time the system can recover data, based on the most recent successful backup or snapshot. Recovery is based on the last successful metadata backup and log archive. There might be a delay between the failure and the restored state.

To strengthen data resilience and minimize potential loss, the backup frequency for the Milvus service in the SaaS environment has been increased. This change reduces the Recovery Point Objective (RPO) to just 2 hours, ensuring that data can be restored from a much more recent point in time in the event of a failure.
{: note}

## Locations
{: #locations}

### AWS Regions
{: #aws_regns}

1. Oregon (us-west-2)
2. N. Virginia (us-east-1)
3. Frankfurt (eu-central-1)
4. Tokyo (jp-tok)

### IBM Regions
{: #ibm_regns}

1. Dallas (us-south)
2. Washington (us-east)
3. Frankfurt (eu-de)
4. London (eu-gb)
5. Tokyo (jp-tok)
6. Sydney (au-syd)
