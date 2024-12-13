---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-13"

keywords: lakehouse, watsonx data, events, audit, activity

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for {{site.data.keyword.lakehouse_short}}
{: #at_events}

The Mezmo backed {{site.data.keyword.at_full_notm}} service is now deprecated in {{site.data.keyword.cloud_notm}} but will continue to be supported until the end of March, 2025, at which point all instances will be removed. It is suggested that you migrate to {{site.data.keyword.cloud_notm}} logs/{{site.data.keyword.at_full_notm}} event routing as soon as possible to avoid disruptions.
{: note}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.cloud_notm}} activity tracking facilities to track how users and applications interact with the {{site.data.keyword.lakehouse_full}} service in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Managing and viewing activities with {{site.data.keyword.at_full}} Event Routing and {{site.data.keyword.cloud_notm}} Logs
{: #at_mng_view_act}

The {{site.data.keyword.at_full_notm}} event routing service routes activity events from all participating services (including {{site.data.keyword.lakehouse_full}}) that are provisioned in an account to its configured targets, such as an instance of {{site.data.keyword.cloud_notm}} logs. These activity events include any user or IBM initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the target services to investigate abnormal activities and critical actions and to comply with regulatory audit requirements. Additionally, you can receive alerts about any activities in real time. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standards.

For more information, see
- [Monitoring activity tracking events in IBM Cloud Logs](https://cloud.ibm.com/docs/cloud-logs?topic=cloud-logs-cl-at-events&interface=ui)
- [sending to IBM Cloud Logs](https://cloud.ibm.com/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).

## Managing and viewing activities with the deprecated {{site.data.keyword.at_full}} service
{: #at_mng_view_act2}

{{site.data.keyword.at_full}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activities and critical actions and to comply with regulatory audit requirements. Additionally, you can receive alerts about any activities in real time. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standards.

For more information, see the [Getting started with IBM Cloud Activity Tracker](https://cloud.ibm.com/docs/activity-tracker?topic=activity-tracker-getting-started).

## Platform events
{: #at_actions_platform}

The following table lists the events generated at watsonx.data (platform) level:

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.lakehouse.create`      | Generated when a watsonx.data instance is provisioned. |
| `lakehouse.presto.create`         | Generated when a Presto (Java) group is provisioned. |
| `lakehouse.hms.create`            | Generated when a metastore is provisioned.|
| `lakehouse.lakehouse.delete`      | Generated when a watsonx.data instance is deleted.|
| `lakehouse.presto.delete`         | Generated when a Presto (Java) group is deleted. |
| `lakehouse.hms.delete`            | Generated when a metastore is deleted. |
{: caption="Actions that generate platform events" caption-side="bottom"}

## Engines events
{: #at_actions_engines}


| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.engines.list`           | Generated when engines are listed. |
{: caption="Lists of engine events" caption-side="bottom"}



## Presto (Java) events
{: #at_presto_engines}


| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.presto_engine.list`      | Generated when all Presto (Java) engines are listed. |
|`lakehouse.presto_engine.create`    | Generated when Presto (Java) engine is created.   |
|`lakehouse.presto_engine.get`       | Generated when Presto (Java) engine details are retrieved.      |
|`lakehouse.presto_engine.delete` | Generated when Presto (Java) engine is deleted.      |
|`lakehouse.presto_engine.update` | Generated when Presto (Java) engine is updated.      |
|`lakehouse.presto_engine.pause` | Generated when Presto (Java) engine is paused.        |
|`lakehouse.presto_engine.resume` | Generated when Presto (Java) engine is resumed.      |
|`lakehouse.presto_engine.scale` | Generated when Presto (Java) engine is scaled.        |
|`lakehouse.presto_engine.refresh` | Generated when Presto (Java) is restarted.           |
|`lakehouse.presto_engine_catalog.add` | Generated when catalog is added to Presto (Java) engine.|
|`lakehouse.instance.list` | Generated when list of deployments is fetched.          |
{: caption="Lists of Presto (Java) engine events" caption-side="bottom"}


## Presto (C++) events
{: #at_prestissimo_engines}


| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.prestissimo_engine.create`  |Generated when Presto (C++) engine is created.|
|`lakehouse.prestissimo_engine.list`  |Generated when all Presto (C++) engines are listed.|
|`lakehouse.prestissimo_engine.get`  |Generated when Presto (C++) engine details are fetched.|
|`lakehouse.prestissimo_engine.delete`  |Generated when Presto (C++) engine is deleted.|
|`lakehouse.prestissimo_engine.update`  |Generated when Presto (C++) engine is updated.|
|`lakehouse.prestissimo_engine.pause`   |Generated when Presto (C++) engine is paused.|
|`lakehouse.prestissimo_engine.resume`   |Generated when Presto (C++) engine is resumed.|
|`lakehouse.prestissimo_engine.scale`   |Generated when Presto (C++) engine is scaled.|
|`lakehouse.prestissimo_engine.refresh`   |Generated when Presto (C++) is restarted.|
|`lakehouse.prestissimo_engine_catalog.add` | Generated when catalog is added to Presto (C++) engine.|
{: caption="Lists of Presto (C++) engine events" caption-side="bottom"}


## Spark engine events
{: #at_actions_spark}

| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.spark_engine.list` | Generated when Spark engines are listed.|
|`lakehouse.spark_engine.create` | Generated when Spark engine is created.|
|`lakehouse.spark_engine.update` | Generated when the details of a Spark engine is updated.|
|`lakehouse.spark_engine.delete` | Generated when a Spark engine is deleted.|
|`lakehouse.spark_engine_application.list` | Generated when the Spark applications under a Spark engine is listed.|
|`lakehouse.spark_engine_application.get`| Generated when the details of a Spark application is listed.|
|`lakehouse.spark_engine_application.create` | Generated when a Spark application is run.|
|`lakehouse.spark_engine_application.delete` | Generated when a running Spark application is stopped.|
|`lakehouse_spark_engine_application.ui`| Generated when the Spark UI of an application is accessed.|
|`lakehouse.spark_engine_history_server.get` | Generated when the Spark history server details are listed.|
|`lakehouse.spark_engine_history_server.start` | Generated when the Spark history server is started.|
|`lakehouse.spark_engine_history_server.stop` | Generated when the Spark history server is stopped.|
|`lakehouse.spark_engine_history_server.ui` | Generated when Spark history UI is accessed.|
|`lakehouse.spark_engine_catalog.list` | Generated when Spark engine associated catalogs are listed.|
|`lakehouse.spark_engine_catalog.add` | Generated when catalogs are associated with a Spark engine.|
|`lakehouse.spark_engine_catalog.remove` | Generated when catalogs are dissociated from a Spark engine.|
|`lakehouse.spark_engine_catalog.get` | Generated when the details of a Spark engine catalog are listed.|
|`lakehouse.spark_engine_cluster.list` | Generated when Spark lab clusters is listed.|
|`lakehouse.spark_engine_cluster.create` | Generated when a Spark lab cluster is created.|
|`lakehouse.spark_engine_cluster.get` | Generated when the details of a Spark lab cluster is retrieved.|
|`lakehouse.spark_engine_cluster.delete` | Generated when a Spark lab cluster is deleted.|
|`lakehouse.spark_engine_cluster.connect` | Generated when a Spark lab cluster is connected.|
|`lakehouse.spark_engine.pause` | Generated when a Spark engine is paused.|
|`lakehouse.spark_engine.resume` | Generated when a Spark engine is resumed.|
|`lakehouse.spark_engine.scale` | Generated when a Spark engine is scaled.|
{: caption="Lists of data policy events" caption-side="bottom"}



## Db2 engine events
{: #at_Db2_engines}


| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.db2_engine.list`     |Generated when all Db2 engines are listed.|
|`lakehouse.db2_engine.create`   |Generated when a new Db2 engine is created.|
|`lakehouse.db2_engine.delete`   |Generated when a Db2 engine is deleted.|
|`lakehouse.db2_engine.update`   |Generated when a Db2 engine is updated.|
{: caption="Lists of Db2 engine events" caption-side="bottom"}


## Netezza engines events
{: #at_Netezza_engines}

| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.netezza_engine.list`|  Generated when all netezza engines are listed.|
|`lakehouse.netezza_engine.create`|  Generated when netezza engine is created.|
|`lakehouse.netezza_engine.delete`|  Generated when netezza engine is deleted.|
|`lakehouse.netezza_engine.update`|  Generated when netezza engine is updated.|
{: caption="Lists of Netezza engine events" caption-side="bottom"}

## Other engine events
{: #at_other_engines}

| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.other_engine.list`|   Generated when other engines are listed.|
|`lakehouse.other_engine.create`|   Generated when other engine is created.|
|`lakehouse.other_engine.delete`| Generated when other engine is deleted.|
{: caption="Lists of other engine events" caption-side="bottom"}


## Storage events
{: #at_actions_buckets}

| Action                            | Description |
|-----------------------------------|-------------|
|`lakehouse.bucket_registration.list`|Generated when list of registered storages are listed.|
|`lakehouse.bucket_registration.create`|Generated when storage is registered.|
|`lakehouse.bucket_registration.get`|Generated when a registered storage is listed.|
|`lakehouse.bucket_registration.update`|Generated when storage is updated.|
|`lakehouse.bucket_registration.delete`|Generated when storage is deregistered.|
|`lakehouse.bucket.object.properties`|Generated when storage object properties are listed.|
|`lakehouse.bucket_registration_object.list`|Generated when storage object is listed.|
|`lakehouse.test_bucket_connection.evaluate`|Generated when storage credential is validated.|
|`lakehouse.bucket_registration_activate.add`|Generated when storage is activated.|
|`lakehouse.bucket_registration_activate.remove`|Generated when storage is deactivated.|
|`lakehouse.storage_hdfs_registration.create`|Generated when HDFS storage is added/created.|
{: caption="Lists of storage events" caption-side="bottom"}



## Catalog events
{: #at_actions_catalogs}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.catalogs.create`       | Generated when a catalog is created. |
| `lakehouse.catalogs.get`          | Generated when catalogs are listed. |
| `lakehouse.catalogs.update`       | Generated when a catalog is updated. |
| `lakehouse.catalogs.delete`       | Generated when a catalog is deleted. |
|`lakehouse.catalog_sync.update`|Generated when the external Iceberg table registration for a catalog is synchronized.|
|`lakehouse.schema.list`|Generated when all schemas in catalog is listed.|
|`lakehouse.schema.create`|Generated when schema is created.|
|`lakehouse.schema.delete`|Generated when schema is deleted.|
|`lakehouse.table.list`|Generated when all tables in a schema in a catalog for a given engine is listed.|
|`lakehouse.table.get`|Generated when details of a given table in a catalog and schema is listed.|
|`lakehouse.table.update`|Generated when table is renamed.|
|`lakehouse.table.delete`|Generated when table is deleted.|
|`lakehouse.table_snapshot.list`|Generated when all table snapshots are listed.|
|`lakehouse.table_rollback.set`|Generated when a rollback is performed to a table snapshot.|
|`lakehouse.column.list`|Generated when all columns of a table is listed.|
|`lakehouse.column.create`|Generated when one or multiple columns to a table in a schema for a given catalog is added.|
|`lakehouse.column.update`|Generated when the given column - rename column is updated.|
{: caption="Lists of catalog events" caption-side="bottom"}



## Database events
{: #at_actions_databases}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.databases.create`      | Generated when a database is created. |
| `lakehouse.databases.get`         | Generated when databases are listed. |
| `lakehouse.databases.update`      | Generated when database is updated. |
| `lakehouse.databases.delete`      | Generated when a database is deleted. |
|`lakehouse.database_registration.list`|Generated when list of databases are retrieved.|
|`lakehouse.database_registration.create`|Generated when a new database is added or created.|
|`lakehouse.database_registration.get`|Generated when a registered database is listed.|
|`lakehouse.database_registration.delete`|Generated when database is deleted.|
|`lakehouse.database_registration.update`|Generated when database is updated.|
|`lakehouse.test_database_connection.evaluate`|Generated when database connection is validated.|
{: caption="Lists of database events" caption-side="bottom"}

## Authentication events
{: #at_actions_authentication}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.authtoken.create`      | Generated when a user logs in. |
| `lakehouse.authtoken.delete`      | Generated when a user logs out. |
{: caption="Lists of events for authentication" caption-side="bottom"}

## Engine user events
{: #at_actions_engine_users}

| Action                            | Description |
|---------------------------------|---------------|
| `lakehouse.engineusers.create`    | Generated when an engine user is created. |
| `lakehouse.engineusers.update`    | Generated when an engine user is updated. |
| `lakehouse.engineusers.delete`    | Generated when an engine user is deleted. |
{: caption="Lists of engine user events" caption-side="bottom"}

## Storage user events
{: #at_actions_bucket_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.bucketusers.create`    | Generated when a bucket user is created. |
| `lakehouse.bucketusers.update`    | Generated when a bucket user is updated. |
| `lakehouse.bucketusers.delete`    | Generated when a bucket user is deleted. |
{: caption="Lists of bucket user events" caption-side="bottom"}

## Catalog user events
{: #at_actions_catalog_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.catalogusers.create`   | Generated when a catalog user is created. |
| `lakehouse.catalogusers.update`   | Generated when a catalog user is updated. |
| `lakehouse.catalogusers.delete`   | Generated when a catalog user is deleted. |
{: caption="Lists of catalog user events" caption-side="bottom"}

## Database connection users events
{: #at_actions_database_connection_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.dbconnusers.create`    | Generated when a database connection user is created. |
| `lakehouse.dbconnusers.update`    | Generated when a database connection user is updated. |
| `lakehouse.dbconnusers.delete`    | Generated when a database connection user is deleted. |
{: caption="Lists of database connection user events" caption-side="bottom"}

## Metastore user events
{: #at_actions_metastore_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.metastoreusers.create` | Generated when a metastore user is created. |
| `lakehouse.metastoreusers.update` | Generated when a metastore user is updated. |
| `lakehouse.metastoreusers.delete` | Generated when a metastore user is deleted. |
{: caption="Lists of metastore user events" caption-side="bottom"}

## Data policy events
{: #at_actions_data_policy}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.datapolicy.create`     | Generated when a data policy is created. |
| `lakehouse.datapolicy.update`     | Generated when a data policy is updated. |
| `lakehouse.datapolicy.delete`     | Generated when a data policy is deleted. |
{: caption="Lists of data policy events" caption-side="bottom"}


## Events for Drivers
{: #at_actions_data_policy}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.driver_registration.create`     | Generated when driver is registered. |
| `lakehouse.driver_registration.list`     | Generated all driver details are listed. |
| `delete_driver_registration`     | Generated when a driver is deleted. |
| `lakehouse.driver_registration_engine.add`     | Generated when a driver is associated with engines. |
{: caption="Lists of Driver events" caption-side="bottom"}
