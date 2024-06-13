---

copyright:
  years: 2022, 2024
lastupdated: "2024-06-12"

keywords: lakehouse, watsonx data, privileges, roles, access

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

# Managing roles and privileges
{: #role_priv}

A role is a set of privileges that is assigned to a user to allow the user to perform and manage certain tasks in {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

{{site.data.keyword.lakehouse_short}} provides a set of predefined roles: Administrator, User, Manager, Writer, and Reader.

Use the **Access control** page to manage users and roles in {{site.data.keyword.lakehouse_short}}. For more information, see [Managing user access](watsonxdata?topic=watsonxdata-manage_access).

The following tables describe the privileges that you can assign to roles and associated permissions:

## Formation, Instance, and Install
{: #formation_instance_install}

### Default admin access
{: #default_admin1}

Formation admins (IAM) have the default admin access.

### Default user access
{: #default_user1}

IAM formation non-admins (Operator, Editor, Viewer) have the default user access.

### Resource-level permissions
{: #rl_premission1}

| Action | Admin | User | Metastore Access |
|-------|------|------|---------|
| Create Presto engines | ✓ |   |    |
| Create or register Spark engines | ✓ |   |    |
| Create Milvus services | ✓ |   |    |
| Delete Milvus services | ✓ |   |    |
| View Milvus services | ✓ |   |    |
| Restart the internal HMS | ✓ |   |    |
| Scale the Presto engines | ✓ |   |    |
| Unregister any bucket | ✓ |   |    |
| Unregister any DB Connection | ✓ |   |    |
| Activate cataloged buckets (restart HMS) | ✓ |   |    |
| Register and unregister own bucket | ✓ | ✓ | ✓ |
| Register and unregister own DB connection | ✓ | ✓ | ✓ |
| Access the metastore | ✓ |   | ✓ |
{: caption="Table 1. Resource-level permissions" caption-side="bottom"}

## Engine (Presto)
{: #engine_presto}

### Default admin access
{: #default_admin2}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission2}

| Action | Admin | Manager | User | Users without an explicit role |
|-------|------|------|---------|---------|
| Delete | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
| Pause and resume | ✓ | ✓ |    |     |
| Restart | ✓ | ✓ |    |     |
| Associate and disassociate catalog | ✓ | ✓ |    |     |
| Access the Presto query monitor UI | ✓ | ✓ |    |     |
| View existence (infra page and `…/api/…/` engines) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Table 2. Resource-level permissions" caption-side="bottom"}

## Engine (External Spark)
{: #external_spark}

### Default admin access
{: #default_admin3}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission3}

| Action | Admin | Manager | User | Users without an explicit role |
|-------|------|------|---------|---------|
| Delete | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
| Update Spark engine metadata (like tags and description) | ✓ | ✓ |    |     |
| Scale Spark engine | ✓ | ✓ |    |     |
| View existence (infra page and `…/api/…/` engines) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Table 3. Resource-level permissions" caption-side="bottom"}

## Engine (Native Spark)
{: #native_spark}

### Default admin access
{: #default_admin3}

Default user access is granted to:

- Formation admins (IAM)
- Instance admins (CPD)
- Install admins (Dev)

### Resource-level permissions
{: #rl_premission4}

| Action | Admin | Manager | User | Users without an explicit role |
|-------|------|------|---------|---------|
|Create and delete engine | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
|Scale engine | ✓ | ✓ |    |     |
| Pause and resume  | ✓ | ✓ |    |     |
| Update Spark engine metadata (like tags and description) | ✓ | ✓ |    |     |
| Update Spark default version | ✓ | ✓ |    |     |
| Update Spark default configuration | ✓ | ✓ |    |     |
| Scale Spark engine | ✓ | ✓ |    |     |
| Start and stop Spark history server | ✓ | ✓ | ✓ |     |
| View Spark history UI | ✓ | ✓ | ✓ |     |
| View Spark UI | ✓ | ✓ | ✓ |     |
| Associate and disassociate catalog | ✓ | ✓ |    |     |
| View existence (infra page and `…/api/…/` engines) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Table 2. Resource-level permissions" caption-side="bottom"}

## Service (Milvus)
{: #milvus}

### Default admin access
{: #default_admin5}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission5}

| Action | Admin | Editor | Viewer | Users without an explicit role | Database creator (Implicit role) | Collection creator (Implicit role) |
| --- | --- | --- | --- | --- | --- | --- |
| View assigned Milvus service | ✓ | ✓ | ✓ |  |  |  |
| Delete assigned Milvus service | ✓ |  |  |  |  |  |
| Grant access to assigned Milvus service | ✓ |  |  |  |  |  |
| Revoke access from assigned Milvus service | ✓ |  |  |  |  |  |
| Collection `CreateIndex` | ✓ | ✓ |  |  |✓| ✓ |
| Collection `DropIndex` | ✓ | ✓ |  |  | ✓ |✓  |
| Global `CreateCollection`  | ✓ | ✓ |  |  | ✓ |  |
| Global `DescribeCollection` | ✓ | ✓ | ✓ |  | ✓ |✓  |
| Global `ShowCollections` | ✓ | ✓ | ✓ |  |✓  |  |
| Collection `CreateAlias` | ✓ | ✓ |  |  |  ✓|  |
| Collection `DropAlias` | ✓ | ✓ |  |  | ✓ |  |
| Collection `DescribeAlias` | ✓ | ✓ | ✓ |  | ✓ |  |
| Collection `ListAliases` | ✓ | ✓ | ✓ |  |  ✓| ✓ |
| Global `FlushAll` | ✓ | ✓ |  |  |  |  |
| Global `CreateResourceGroup` | ✓ |  |  |  |  |  |
| Global `DropResourceGroup` | ✓ |  |  |  |  |  |
| Global `DescribeResourceGroup` | ✓ |  |  |  |  |  |
| Global `ListResourceGroups` | ✓ |  |  |  |  |  |
| Global `TransferNode` | ✓ |  |  |  |  |  |
| Global `TransferReplica` | ✓ |  |  |  |  |  |
| Global `CreateDatabase` | ✓ | ✓ |  |  |   |  |
| Global `DropDatabase` | ✓ | ✓ |  |  |  |  |
| Global `ListDatabases` | ✓ | ✓ | ✓ |  |  |  |
| Collection `IndexDetail` | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| Collection `Search` | ✓ | ✓ | ✓ |  | ✓ |✓  |
| Collection `Query` | ✓ | ✓ | ✓ |  | ✓ |✓  |
| Collection `Load` | ✓ | ✓ |  |  | ✓ |✓  |
| Collection `GetLoadState` | ✓ | ✓ |  |  |  ✓| ✓ |
| Collection `Release` | ✓ | ✓ |  |  | ✓ |  ✓|
| Collection `RenameCollection` | ✓ | ✓ |  |  |✓  | ✓ |
| Collection `DropCollection` | ✓ | ✓ |  |  | ✓ |✓  |
| Collection `Insert` | ✓ | ✓ |  |  | ✓ |  ✓|
| Collection `Delete` | ✓ | ✓ |  |  | ✓ |  ✓|
| Collection `Flush` | ✓ | ✓ |  |  | ✓ | ✓ |
| Collection `GetFlushState` | ✓ | ✓ |  |  | ✓ |✓  |
| Collection `Upsert` | ✓ | ✓ |  |  | ✓ |✓  |
| Collection `GetStatistics` | ✓ | ✓ |  |  | ✓ | ✓ |
| Collection `Compaction` | ✓ | ✓ |  |  | ✓ | ✓ |
| Collection `Import` | ✓ | ✓ |  |  | ✓ |  ✓|
| Collection `LoadBalance` | ✓ | ✓ |  |  | ✓ | ✓ |
| Collection `CreatePartition` | ✓ | ✓ |  |  |  ✓| ✓ |
| Collection `DropPartition` | ✓ | ✓ |  |  | ✓ |✓  |
| Collection `ShowPatitions` | ✓ | ✓ | ✓ |  | ✓ |✓  |
| Collection `HasPatition` | ✓ | ✓ | ✓ |  |✓  | ✓ |
{: caption="Table 4. Resource-level permissions" caption-side="bottom"}

## Bucket
{: #bucket}

### Default admin access (only if creator)
{: #default_admin6}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission6}

| Action | Admin | Writer | Reader | Users without an explicit role |
|-------|------|------|---------|---------|
| Unregister | ✓ |   |    |     |
| Update bucket properties (credentials) | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
| Modify files | ✓ | ✓ |    |     |
| Browse (bucket browser in UI) | ✓ | ✓ | ✓ |     |
| View existence (infra page and `…/api/…/` buckets) | ✓ | ✓ | ✓ | ✓ |
{: caption="Table 5. Resource-level permissions" caption-side="bottom"}

If you want to unregister or delete a bucket, you must first deactivate the bucket.
{: note}

#### S3 REST API permissions (specific to IBM Spark and CAS proxy)
{: #s3restapi}

Users can get relative bucket role for all sub-folders and files in a bucket or can be granted file action for particular folders or files. The following tables explain the bucket-level and data-object-level S3 REST API permissions.

The following tables are applicable only if you are using IBM Spark that by default uses a CAS signature or if you are using CAS proxy.
{: note}

| Bucket role | S3 REST API permission |
| --- | --- |
| Reader | GET; HEAD; PUT; POST; PATCH; DELETE |
| Writer | GET; HEAD |
| Admin | GET; HEAD; PUT; POST; PATCH; DELETE |
{: caption="Table 6. Bucket level access control in Access control > Infrastructure or Infrastructure manger > select bucket and assign roles" caption-side="bottom"}

| Data object action | S3 REST API permission |
| --- | --- |
| Read | GET; HEAD |
| Write | GET; HEAD; PUT; PATCH; POST without `?delete` parameter |
| Delete | DELETE; POST with `?delete` parameter |
{: caption="Table 7. Data-object-level access control in Access control > Policies" caption-side="bottom"}

## Database
{: #db_connection}

### Default admin access (only if creator)
{: #default_admin7}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission7}

| Action | Admin | Writer | Reader | Users without an explicit role |
|-------|------|------|---------|---------|
| Unregister | ✓ |   |    |     |
| Update `db conn` properties (credentials) | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
| Modify database objects | ✓ | ✓ |    |     |
| View existance (infra page and `…/api/…/extdb`) | ✓ | ✓ | ✓ | ✓ |
{: caption="Table 8. Resource-level permissions" caption-side="bottom"}

## Catalog
{: #catalog}

### Default admin access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_admin8}

Formation admins (IAM) have the default admin access.

### Default user access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_user8}

IAM formation non-admins (Operator, Editor, Viewer) have the Default user access.

### Resource-level permissions
{: #rl_premission8}

| Action | Admin | User | Users without an explicit role |
|-------|------|------|---------|
| Delete | ✓ |   |     |
| Grant and revoke access | ✓ |   |     |
| Access to data | ✓ | Based on data policy |     |
| View existence (infra page and `…/`) | ✓ | ✓ |     |
{: caption="Table 9. Resource-level permissions" caption-side="bottom"}

## Schema
{: #schema}

### Default admin access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_admin9}

Formation admins (IAM) have the default admin access.

### Default user access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_user9}

IAM formation non-admins (Operator, Editor, Viewer) have the Default user access.

### Resource-level permissions
{: #rl_premission9}

| Action | Catalog Admin or schema creator | Others |
|-------|------|------|
| Grant and revoke access | ✓ |   |
| Drop | ✓ |   |
| Access | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Create table | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
{: caption="Table 10. Resource-level permissions" caption-side="bottom"}

## Table
{: #table}

### Default admin access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_admin10}

Formation admins (IAM) have the default admin access.

### Default user access (based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin)
{: #default_user10}

IAM formation non-admins (Operator, Editor, Viewer) have the Default user access.

### Resource-level permissions
{: #rl_premission10}

| Action | Catalog Admin or schema admin or table creator | Others |
|-------|------|------|
| Create, drop, and alter | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Column access | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Select | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Insert | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Update | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
| Delete | ✓ | based on access data control policies defined in {{site.data.keyword.lakehouse_short}} by admin |
{: caption="Table 11. Resource-level permissions" caption-side="bottom"}
