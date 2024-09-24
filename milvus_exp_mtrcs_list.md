---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

keywords: lakehouse, milvus, watsonx.data

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

# Metrics exposed by Milvus
{: #milvus_exp_metrics_list}

The following tables cover the metrics that are exposed by Milvus.

## Proxy
{: #milvus_exp_metrics_list_proxy}

| Metrics name | Metrics type | Description |
| --- | --- | --- |
| milvus_proxy_search_vectors_count | counter | The accumulated number of vectors queried (search). |
| milvus_proxy_insert_vectors_count | counter | The accumulated number of vectors inserted. |
| milvus_proxy_sq_latency_sum | Counter | The average latency between sending search and query requests and receiving results by proxy. |
| milvus_proxy_sq_wait_result_latency_bucket | Histogram | The latency of aggregating search and query results by proxy. |
| milvus_proxy_sq_reduce_result_latency_bucket | Histogram | The latency of aggregating search and query results by proxy.|
| milvus_proxy_sq_decode_result_latency_bucket | Histogram | The latency of decoding search and query results by proxy. |
| Milvus_proxy_collection_sq_latency_sum | Counter | The latency of search and query requests to a specific collection. |
| milvus_proxy_mutation_send_latency_bucket | Histogram | The latency of sending insertion or deletion requests by each proxy. |
| milvus_proxy_cache_hit_count | Counter | The average cache hit rate of operations including GeCollectionID, GetCollectionInfo, and GetCollectionSchema. |
| milvus_proxy_cache_update_latency_bucket | Histogram | The cache update latency by proxy. |
| milvus_proxy_apply_pk_latency_bucket | Histogram | The primary key application latency by each proxy. |
| milvus_proxy_apply_timestamp_latency_bucket | Histogram | The timestamp application latency by each proxy. |
| milvus_proxy_req_count | Counter | The number of all types of receiving requests. |
| milvus_proxy_req_latency_sum | Counter | The latency of all types of receiving requests by each proxy. |
| milvus_proxy_receive_bytes_count | Counter | The number of bytes of insert and delete requests that are received by proxy. |
| milvus_proxy_send_bytes_count | Counter | The number of bytes per second sent back to the client while each proxy is responding to search and query requests. |
| Milvus_proxy_mutation_latency_sum | Sum | The latency of mutation requests. In Milvus, a mutation request refers to operations that modify the data in a collection. These operations include the following: 1. **Insert**: Adding new vectors (data points) into a collection. Each vector usually comes with an associated unique identifier (ID) and optional metadata. 2. **Delete**: Removing vectors from a collection based on their unique identifiers. This operation marks vectors as deleted but does not immediately remove them from the disk. The actual deletion is handled later during a compaction process. 3. **Update (Upsert)**: Although Milvus traditionally supports only **Insert** and **Delete** operations, recent versions support update operations, where existing vectors are replaced or updated with new data. This involves a combination of **Insert** and **Delete** operations. |
| milvus_proxy_sq_wait_result_latency_sum | Counter | The latency between sending search and query requests and receiving results this value is determined between dividing the sum/count of the milvus_proxy_sq_wait_result_latency_bucket histogram. |
| milvus_proxy_msgstream_obj_num | Gauge | The number of msgstream objects created on each physical topic. |
{: caption="Table 1. Proxy" caption-side="bottom"}

## Root coordinator
{: #milvus_exp_metrics_list_rc}

| Metrics name | Metrics type | Description |
| --- | --- | --- |
| milvus_rootcoord_proxy_num | Gauge | The number of proxies created. Since root coord has 1 replica, the number of proxy node is 1. |
| milvus_rootcoord_ddl_req_count | Counter | DDL request rate - The total number of DDL requests including `CreateCollection`, `DescribeCollection`, `DescribeSegments`, `HasCollection`, `ShowCollections`, `ShowPartitions`, and `ShowSegments`. |
| milvus_rootcoord_ddl_req_latency_bucket | Histogram | DDL request latency - The latency of all types of DDL requests. Several factors can influence the latency of DDL requests like system load, network conditions, complexity of the DDL operation, and the size of the collection or partition being manipulated. Monitoring DDL request latency is an important aspect of maintaining optimal performance in a Milvus deployment. It helps in identifying and addressing potential issues that could affect the overall system efficiency. |
| milvus_rootcoord_sync_timetick_latency_bucket | Histogram | Sync timetick latency - The time used by root coord to sync all timestamp to `pchannel`. In Milvus, a `pchannel` (physical channel) is a component of the message queue system used for data processing and time synchronization. Milvus assigns a `pchannel` to each virtual channel (`vchannel`) in the log broker. This assignment is part of the data insertion process. When you create a collection in Milvus, you can specify a number of shards. Each shard corresponds to a `vchannel`. Milvus then assigns each `vchannel` to a `pchannel` in the log broker. The root coordinator plays a crucial role in time synchronization across the system. The root coordinator identifies the minimum timestamp value on each `MsgStream`, regardless of which proxy the `InsertMsgs` belong to. It then inserts this minimum timestamp (also called a timetick) into the `MsgStream`. When consumer components read the timetick inserted by the root coordinator, they understand that all insert messages with smaller timestamp values have been consumed. This process ensures that all operations across different nodes are kept in order, addressing issues like time clock differences between nodes, and network latency. |
| milvus_rootcoord_id_alloc_count | Counter | ID allocation rate - The accumulated number of IDs assigned by root coord. |
| milvus_rootcoord_timestamp | Gauge | Timestamp - The latest timestamp of root coord. |
| milvus_rootcoord_timestamp_saved | Gauge | Timestamp saved - The pre-assigned timestamps that root coord saves in meta storage. |
| milvus_rootcoord_collection_num | Gauge | Collection number - The total number of collections existing in Milvus currently. |
| milvus_rootcoord_partition_num | Gauge | Partition number - The total number of partitions existing in Milvus currently. |
| milvus_rootcoord_dml_channel_num | Gauge | DML channel number - The total number of DML channels existing in Milvus currently. A DML channel in Milvus refers to a communication channel used for Data Manipulation Language operations. 1 DML operations include insert, delete, and upsert actions in the database. In Milvus, a DML channel is equivalent to a virtual channel (`vchannel`). The system uses a structure where: A physical channel (`pchannel`) is bound to a topic in message queue systems like Pulsar or Kafka. - A `vchannel` is like a logical connection between two components within the system. The DML channel serves several important functions in Milvus: 1. **Data Distribution**: It's used to route incoming insert/delete requests to appropriate shards based on the hash value of primary keys. 2 **Message publishing**: The proxy publishes DML messages through this channel. 3. **Data processing**: Both data nodes and query nodes subscribe to the DML channel to process operations and provide search and query services. |
| milvus_rootcoord_msgstream_obj_num | Gauge | `Msgstream` number - The total number of `msgstream` in Milvus currently. |
| milvus_rootcoord_credential_num | Gauge | Credential number - The total number of credentials in Milvus currently. |
{: caption="Table 2. Root coordinator" caption-side="bottom"}

## Data coordinator
{: #milvus_exp_metrics_list_dc}

| Metrics-Name | Metrics type | Description |
| --- | --- | --- |
| milvus_datacoord_datanode_num | Gauge | The number of data nodes managed by data coord. |
| milvus_datacoord_segment_num | Gauge | The number of all types of segments recorded in metadata by data coord. |
| milvus_datacoord_collection_num | Gauge | The number of collections recorded in metadata by data-coord. |
| milvus_datacoord_stored_row_num | Gauge | The total number of rows by collection. |
| milvus_datacoord_stored_binlog_size | Gauge | The total size of stored binlog. |
{: caption="Table 3. Data coordinator" caption-side="bottom"}

## Query coordinator
{: #milvus_exp_metrics_list_qc}

| Metrics-Name | Metrics Type | Description |
| --- | --- | --- |
| milvus_querycoord_collection_num | Gauge | The number of collections that are currently loaded by Milvus. |
| milvus_querycoord_load_req_count | Counter | The accumulated number of load requests including the status of the job. |
| milvus_querycoord_release_req_count | Counter | The number of release requests. |
| milvus_querycoord_load_latency_bucket | Histogram | The average latency, the 99th percentile of load request latency within the past two minutes, and the time used to complete a load request. |
| milvus_querycoord_load_latency_sum | Counter | The time used to complete a load request. |
| milvus_querycoord_release_latency_bucket | Histogram | The time used to complete a release request. |
| milvus_querycoord_release_latency_sum | Counter | The latency of release request. |
{: caption="Table 4. Query Coordinator" caption-side="bottom"}
