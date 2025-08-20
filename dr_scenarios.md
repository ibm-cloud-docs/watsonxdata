---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-20"

keywords: high availability, disaster revecory, watsonx.data

subcollection: watsonxdata

---



{{site.data.keyword.attribute-definition-list}}

# Disaster scenarios in {{site.data.keyword.lakehouse_short}}
{: #dr_scenarios}

## Scenario 1: Kubernetes configuration corruption
{: #dr_scenarios_1}

**Description**: Corruption or deletion of formations, ConfigMaps, Secrets, and more.

- **General impact**:
  - SRE receives alerts and restores the Kubernetes configurations or formations.
  - Inflight queries fail, resulting in a temporary outage.
  - RTO and RPO are reviewed with SRE.

- **Milvus**:
  - Inflight queries and data ingestion fail.
  - SRE restores the formation from backup.
  - Temporary outage; RPO and RTO are updated.

- **Presto**:
  - Inflight queries and ingestion fail.
  - Formation restored from backup.

- **MDS**:
  - Inflight API calls fail.
  - Outage until formation is restored.
  - Velero backup ensures service restoration, but rare port conflicts might require manual service edits.

- **Spark**:
  - Only workloads tied to corrupted configurations fail.
  - Other workloads continue.
  - Users must rerun failed jobs.

- **Customer Involvement**: None



## Scenario 2: Persistent storage corruption
{: #dr_scenarios_2}

**Description**: Corruption of persistent volumes.

- **General Impact**:
  - Services using PVCs are affected.

- **Milvus**:
  - PVC restored from backup.
  - Temporary outage due to ETCD downtime.
  - No data loss.

- **Presto, MDS, Spark**:
  - No impact (do not use PVCs).

- **Customer involvement**: None



## Scenario 3: Data or Metadata corruption
{: #dr_scenarios_3}

**Description**: Corruption of stored data or metadata.

- **General impact**:
  - Service outages during recovery.

- **Milvus**:
  - ETCD metadata restored from hourly backups.
  - Potential loss of up to 1 hour of metadata.
  - Customer responsible for vector storage backups.

- **Presto**:
  - Point-in-time backups used to restore configuration and metadata.

- **MDS, Spark**:
  - No impact.

- **Customer Involvement**: None



## Scenario 4: Cluster failure
{: #dr_scenarios_4}

**Description**: Complete failure of the cluster.

- **Milvus**:
  - Formation and data restored from backup.
  - Possible 1-hour metadata loss.
  - Customer responsible for vector storage backups.

- **Presto**:
  - Formation and data restored from backup.

- **MDS**:
  - Inflight API calls fail.
  - Outage until cluster or formation is restored.

- **Spark**:
  - All running workloads fail.
  - No data loss.
  - SRE restores formation on a new cluster.
  - Users must rerun failed jobs.

- **Customer Involvement**: None



## Scenario 5: Availability Zone (AZ) outage
{: #dr_scenarios_5}

**Description**: One AZ becomes unavailable.

- **General Impact**:
  - Cluster has capacity to migrate workloads.
  - Pods are automatically rescheduled to healthy AZs.

- **Milvus**:
  - Metadata is Active-Active in Enterprise plan.
  - Inflight queries fail; no long-term impact.

- **Presto**:
  - Pods rescheduled; inflight queries fail.

- **MDS**:
  - If only one AZ is down, no impact.
  - If two or more AZs are down, service is impacted until at least one AZ is restored.

- **Spark**:
  - Workloads with drivers in the failed AZ fail.
  - Executors recover in healthy AZs.
  - No impact on workloads in unaffected AZs.

- **Customer Involvement**: None



## Scenario 6: Regional disaster
{: #dr_scenarios_6}

**Description**: Entire region becomes unavailable.

- **Milvus**:
  - Customer provisions a new {{site.data.keyword.lakehouse_short}} instance ouse and Milvus formation in another region.
  - Same bucket and path must be used.
  - Customer shares CRNs of old and new formations.
  - SRE restores ETCD metadata.

- **Presto**:
  - Customer provisions new formation.
  - SRE restores metadata and console DB.

- **MDS**:
  - If hourly Postgres backups are enabled, restore to a new DB instance.
  - Update MDS pod environment variables to point to the new DB.
  - RPO: 1 hour; RTO: 2–3 hours.
  - Console DB and AMS DB also impacted.

- **Spark**:
  - All running workloads fail.
  - Customer provisions a new watsonx.data instance and Spark engine.
  - No data loss (logs or events in object store).

- **Customer Involvement**:
  - Provision new formations and share CRNs.

  Milvus uses Kafka in Active-Active mode (Enterprise plan), so no customer action is needed for Kafka recovery.
{: note}
