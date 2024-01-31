---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-31"

keywords: lakehouse, watsonx data, events, audit, activity

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for {{site.data.keyword.lakehouse_short}}
{: #at_events}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full}} service to track how users and applications interact with the {{site.data.keyword.lakehouse_full}} service in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## List of platform events
{: #at_actions_platform}

The following table lists the actions that generate an event:

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.lakehouse.create`      | An event is generated when you provision a service instance. |
| `lakehouse.presto.create`         | An event is generated when you provision a Presto group. |
| `lakehouse.hms.create`            | An event is generated when you provision a metastore.|
| `lakehouse.lakehouse.delete`      | An event is generated when a service instance is deleted.|
| `lakehouse.presto.delete`         | An event is generated when a when a Presto group is deleted. |
| `lakehouse.hms.delete`            | An event is generated when a metastore is deleted. |
{: caption="Table 1. Actions that generate platform events" caption-side="bottom"}

## Events for engines
{: #at_actions_engines}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.engines.create`        | An event is generated when you create an engine. |
| `lakehouse.engines.get`           | An event is generated when you get engines. |
| `lakehouse.engines.update`        | An event is generated when you update an engine. |
| `lakehouse.engines.delete`        | An event is generated when you delete an engine. |
| `lakehouse.engines.pause`         | An event is generated when you pause an engine. |
| `lakehouse.engines.resume`        | An event is generated when you resume an engine. |
{: caption="Table 2. Lists of engine events" caption-side="bottom"}


## Events for buckets
{: #at_actions_buckets}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.buckets.create`        | An event is generated when you create a bucket. |
| `lakehouse.buckets.get`           | An event is generated when you get buckets. |
| `lakehouse.buckets.update`        | An event is generated when you update a bucket. |
| `lakehouse.buckets.delete`        | An event is generated when you delete a bucket. |
| `lakehouse.buckets.activate`      | An event is generated when you activate a bucket. |
{: caption="Table 3. Lists of bucket events" caption-side="bottom"}

## Events for catalogs
{: #at_actions_catalogs}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.catalogs.create`       | An event is generated when you create a catalog. |
| `lakehouse.catalogs.get`          | An event is generated when you get catalogs. |
| `lakehouse.catalogs.update`       | An event is generated when you update a catalog. |
| `lakehouse.catalogs.delete`       | An event is generated when you delete a catalog. |
{: caption="Table 1. Lists of catalog events" caption-side="bottom"}

## Events for databases
{: #at_actions_databases}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.databases.create`      | An event is generated when you create a database. |
| `lakehouse.databases.get`         | An event is generated when you get databases. |
| `lakehouse.databases.update`      | An event is generated when you update a database. |
| `lakehouse.databases.delete`      | An event is generated when you delete a database. |
{: caption="Table 4. Lists of database events" caption-side="bottom"}

## Events for authentication
{: #at_actions_authentication}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.authtoken.create`      | An event is generated when a user logs in. |
| `lakehouse.authtoken.delete`      | An event is generated when a user logs out. |
{: caption="Table 5. Lists of events for authentication" caption-side="bottom"}

## Events for engine users
{: #at_actions_engine_users}

| Action                            | Description |
|---------------------------------|---------------|
| `lakehouse.engineusers.create`    | An event is generated when you create an engine user. |
| `lakehouse.engineusers.update`    | An event is generated when you update an engine user. |
| `lakehouse.engineusers.delete`    | An event is generated when you delete an engine user. |
{: caption="Table 6. Lists of engine user events" caption-side="bottom"}

## Events for bucket users
{: #at_actions_bucket_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.bucketusers.create`    | An event is generated when you create a bucket user. |
| `lakehouse.bucketusers.update`    | An event is generated when you update a bucket user. |
| `lakehouse.bucketusers.delete`    | An event is generated when you delete a bucket user. |
{: caption="Table 7. Lists of bucket user events" caption-side="bottom"}

## Events for catalog users
{: #at_actions_catalog_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.catalogusers.create`   | An event is generated when you create a catalog user. |
| `lakehouse.catalogusers.update`   | An event is generated when you update a catalog user. |
| `lakehouse.catalogusers.delete`   | An event is generated when you delete a catalog user. |
{: caption="Table 8. Lists of catalog user events" caption-side="bottom"}

## Events for database connection users
{: #at_actions_database_connection_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.dbconnusers.create`    | An event is generated when you create a database connection user. |
| `lakehouse.dbconnusers.update`    | An event is generated when you update a database connection user. |
| `lakehouse.dbconnusers.delete`    | An event is generated when you delete a database connection user. |
{: caption="Table 9. Lists of database connection user events" caption-side="bottom"}

## Events for metastore users
{: #at_actions_metastore_users}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.metastoreusers.create` | An event is generated when you create a metastore user. |
| `lakehouse.metastoreusers.update` | An event is generated when you update a metastore user. |
| `lakehouse.metastoreusers.delete` | An event is generated when you delete a metastore user. |
{: caption="Table 10. Lists of metastore user events" caption-side="bottom"}

## Events for data policy
{: #at_actions_data_policy}

| Action                            | Description |
|-----------------------------------|-------------|
| `lakehouse.datapolicy.create`     | An event is generated when you create a data policy. |
| `lakehouse.datapolicy.update`     | An event is generated when you update a data policy. |
| `lakehouse.datapolicy.delete`     | An event is generated when you delete a data policy. |
{: caption="Table 11. Lists of data policy events" caption-side="bottom"}
