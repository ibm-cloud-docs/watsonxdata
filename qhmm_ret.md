---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-26"

keywords: watsonxdata, qhmm

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

# Retrieving QHMM logs by using ibm-lh utility
{: #qhmm_ret}

The **ibm-lh** utility allows you to retrieve the QHMM logs (provide insights into query executions, enabling users to monitor and analyze performance metrics) without running SQL queries. It can be used to easily retrieve the following query information with the help of keywords.

* Basic query information
* Basic error information of failed queries
* Query stats information
* Query memory information
* Query garbage collection information
* Top time taken query


## Procedure
{: #qhmm1_ret}

1. Install `ibm-lh` client package. For information, see [Installing ibm-lh-client package](https://www.ibm.com/docs/SSDZ38_2.2.x/wxd-client/topics/install-lh-client.html).

1. Use the `cert-mgmt` utility to add or remove SSL certificates in the ibm-lh-client truststore to establish connection with the Presto engine.

   ```bash
   ./cert-mgmt --op=add --host=<saas_host> --port=<port>
   ```
   {: codeblock}

1. Establish connection to {{site.data.keyword.lakehouse_short}} using `ibm-lh-client` package utilities.

   ```bash
   ./connect-lh --op=add --name=<your_saas_name> --host=<saas_host> --port=<port> --username=<your_username> --password=<your_password>
   ```
   {: codeblock}

   For more information, see [Establishing cconnection](https://www.ibm.com/docs/SSDZ38_2.2.x/wxd-client/topics/work-ibm-lh.html).

1. Configure Presto details by using the following command:

   ```bash
   ./ibm-lh config add_saas --name <your_saas_username> --crn <your_crn> --host <saas_host> --port <port> --prestohost <presto_host> --prestoport <presto_port> --username <your_username> --password <your_password>
   ```
   {: codeblock}

1. Select the current instance.

   ```bash
   ./ibm-lh config select --current_instance <your_saas_username>
   ```
   {: codeblock}


1. Use the `ibm-lh monitor qhmm` utility command to retrieve the QHMM logs. For more information about the syntax and the different keywords, see [ibm-lh monitor qhmm](https://www.ibm.com/docs/SSDZ38_2.2.x/wxd-client/topics/ibm_lh_commands.html).

   The syntax is
   ./ibm-lh monitor qhmm --type <type_name> --start-time <start_time> --end-time <end_time> --user <user_id> --query-id <query_id> --query-state <query_state>


Parameters:
* --type <type_name>: Specifies the type of query (e.g., query_failed_info, query_basic_info, query_stats_info, query_memory_info, query_gc_info).
* --start-time <start_time>: Starting timestamp in YYYY-MM-DD HH:MM:SS (UTC).
* --end-time <end_time>: Ending timestamp (optional).
* --user <user_id>: User ID associated with the queries (optional).
* --query-id <query_id>: Specific query ID (optional).
* --query-state <query_state>: State of the query (e.g., COMPLETED, FAILED) (optional).
* --limit <limit_value>: Number of rows to return (optional).
* --order: Name of columns for sorting (optional).


Sample query to retrieve basic information about all queries executed:

`./ibm-lh monitor qhmm --type query_basic_info --start-time "2023-10-01 00:00:00" --end-time "2023-10-08 23:59:59" --user "user123"`

This command fetches basic information for queries executed by `user123` between October 1st and October 8th, 2023.
