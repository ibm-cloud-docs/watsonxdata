---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-17"

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

Use the **Access control** page to manage users and roles in {{site.data.keyword.lakehouse_short}}. For more information, see [Managing user access]({{site.data.keyword.ref-manage_access-link}}).

The following tables describe the privileges that you can assign to roles and associated permissions:

## Instance and Install
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
| Create Presto (Java) or Presto (C++) engines | ✓ |   |    |
| Create or register Spark engines | ✓ |   |    |
| Create Milvus services | ✓ |   |    |
| Delete Milvus services | ✓ |   |    |
| View Milvus services | ✓ |   |    |
| Restart the internal MDS | ✓ |   |    |
| Scale the Presto (Java) or Presto (C++) engines | ✓ |   |    |
| Unregister any storage | ✓ |   |    |
| Unregister any DB Connection | ✓ |   |    |
| Activate cataloged storagees (restart MDS) | ✓ |   |    |
| Register and unregister own storage | ✓ | ✓ | ✓ |
| Register and unregister own DB connection | ✓ | ✓ | ✓ |
| Access the metastore | ✓ |   | ✓ |
| Run Spark ingestion jobs| ✓ |  | ✓ |
{: caption="Resource-level permissions" caption-side="bottom"}

## Engine (Presto (Java) or Presto (C++))
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
| Access the Presto (Java) or Presto (C++) query monitor UI | ✓ | ✓ |    |     |
| View (UI and API) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Resource-level permissions" caption-side="bottom"}

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
| View (UI and API) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Resource-level permissions" caption-side="bottom"}

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
| View (UI and API) | ✓ | ✓ | ✓ |     |
| Run workloads against the engine | ✓ | ✓ | ✓ |     |
{: caption="Resource-level permissions" caption-side="bottom"}

## Service (Milvus)
{: #milvus}

### Default admin access
{: #default_admin5}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission5}

| Action | Admin | Editor | Viewer | User | Database creator (implicit role) | Collection creator (implicit role) | Partition creator (implicit role) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| View assigned Milvus service | ✓ | ✓ | ✓ | ✓ |  |  |  |
| Delete assigned Milvus service | ✓ |  |  |  |  |  |  |
| Grant access to assigned Milvus service | ✓ |  |  |  |  |  |  |
| Revoke access from assigned Milvus service | ✓ |  |  |  |  |  |  |
| Pause Milvus service | ✓ |  |  |  |  |  |  |
| Resume Milvus service | ✓ |  |  |  |  |  |  |
| Collection `CreateIndex` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `DropIndex` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `DescribeCollection` | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |
| Global `CreateCollection` | ✓ | ✓ |  |  | ✓ |  |  |
| Global `ShowCollections` | ✓ | ✓ | ✓ |  | ✓ |  |  |
| Global `CreateAlias` | ✓ | ✓ |  |  | ✓ |  |  |
| Global `DropAlias` | ✓ | ✓ |  |  | ✓ |  |  |
| Global `DescribeAlias` | ✓ | ✓ | ✓ |  | ✓ |  |  |
| Global `ListAliases` | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |
| Global `FlushAll` | ✓ | ✓ |  |  |  |  |  |
| Global `CreateResourceGroup` | ✓ |  |  |  |  |  |  |
| Global `DropResourceGroup` | ✓ |  |  |  |  |  |  |
| Global `DescribeResourceGroup` | ✓ |  |  |  |  |  |  |
| Global `ListResourceGroups` | ✓ |  |  |  |  |  |  |
| Global `TransferNode` | ✓ |  |  |  |  |  |  |
| Global `TransferReplica` | ✓ |  |  |  |  |  |  |
| Global `CreateDatabase` | ✓ | ✓ |  |  |  |  |  |
| Global `DropDatabase` | ✓ | ✓ |  |  | ✓ |  |  |
| Global `ListDatabases` | ✓ | ✓ | ✓ |  |  |  |  |
| Collection `IndexDetail` | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |
| Collection `Search` | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ |
| Collection `Query` | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ |
| Collection `Load` | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |
| Collection `GetLoadingProgress` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `GetLoadState` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `Release` | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |
| Collection `RenameCollection` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `DropCollection` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `Insert` | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |
| Collection `Delete` | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |
| Collection `Flush` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `GetFlushState` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `Upsert` | ✓ | ✓ |  |  | ✓ | ✓ | ✓ |
| Collection `GetStatistics` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `Compaction` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `Import` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `LoadBalance` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `CreatePartition` | ✓ | ✓ |  |  | ✓ | ✓ |  |
| Collection `DropPartition` | ✓ | ✓ |  |  | ✓ | ✓ | ✓  |
| Collection `ShowPartitions` | ✓ | ✓ | ✓ |  | ✓ | ✓ |   |
| Collection `HasPartition` | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓  |
{: caption="Resource-level permissions" caption-side="bottom"}

## storage
{: #bucket}

### Default admin access (only if creator)
{: #default_admin6}

Formation admins (IAM) have the default admin access.

### Resource-level permissions
{: #rl_premission6}

| Action | Admin | Writer | Reader | Users without an explicit role |
|-------|------|------|---------|---------|
| Unregister | ✓ |   |    |     |
| Update storage properties (credentials) | ✓ |   |    |     |
| Grant and revoke access | ✓ |   |    |     |
| Modify files | ✓ | ✓ |    |     |
| Browse (storage browser in UI) | ✓ | ✓ | ✓ |     |
| View (UI and API) | ✓ | ✓ | ✓ | ✓ |
{: caption="Resource-level permissions" caption-side="bottom"}

If you want to unregister or delete a storage, you must first deactivate the storage.
{: note}

#### S3 REST API permissions (specific to IBM Spark and S3 proxy)
{: #s3restapi}

Users can get relative storage role for all sub-folders and files in a storage or can be granted file action for particular folders or files. The following tables explain the storage-level and data-object-level S3 REST API permissions.

The following tables are applicable only if you are using IBM Spark that by default uses an S3 signature or if you are using S3 proxy.
{: note}

| storage role | S3 REST API permission |
| --- | --- |
| Writer |GET; HEAD; PUT; POST; PATCH; DELETE  |
| Reader |GET; HEAD  |
| Admin | GET; HEAD; PUT; POST; PATCH; DELETE |
{: caption="storage level access control in Access control > Infrastructure or Infrastructure manger > select storage and assign roles" caption-side="bottom"}

| Data object action | S3 REST API permission |
| --- | --- |
| Read | GET; HEAD |
| Write | GET; HEAD; PUT; PATCH; POST without `?delete` parameter |
| Delete | DELETE; POST with `?delete` parameter |
{: caption="Data-object-level access control in Access control > Policies" caption-side="bottom"}

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
| View (UI and API) | ✓ | ✓ | ✓ | ✓ |
{: caption="Resource-level permissions" caption-side="bottom"}

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
| View (UI and API) | ✓ | ✓ |     |
{: caption="Resource-level permissions" caption-side="bottom"}

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
{: caption="Resource-level permissions" caption-side="bottom"}

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
{: caption="Resource-level permissions" caption-side="bottom"}
