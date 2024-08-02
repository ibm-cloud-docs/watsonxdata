---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

keywords: watsonxdata, troubleshoot, case sensitivity

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

## Updating the configuration settings for Query Optimizer
{: #ts_optimizer}

### What’s happening
{: #ts_optimizer1}

The configuration settings for Query Optimizer might not be updated resulting in a poor performance of Query Optimizer.

### Why it’s happening
{: #ts_optimizer2}

The query results are not optimized since the configuration settings were not updated resulting in a unoptimized output.

### How to fix it
{: #ts_optimizer3}

You have to verify and update the configuration settings for Query Optimizer to improve the performance of Query Optimizer.

1. Run the following commands to login to the container and apply configuration settings:

   ```bash
   oc exec -it c-lakehouse-oaas-db2u-0 -n ${PROJECT_CPD_INST_OPERANDS} -- sh
   ```
   {: codeblock}

1. Verify that the following registry variable settings and OAAS db configuration settings are updated. If the variables are not updated, do the following additional settings:

   a. Registry variable settings

      i. Run the following command to get the existing registry variable settings:

         ```bash
         su - ${DB2INSTANCE}
         db2 connect to ${DBNAME}
         db2set
         ```
         {: codeblock}

      ii. Update the values as follows if they are not updated:

        ```bash
         db2set DB2_ENABLE_PRESTO_MODE=true
         db2set DB2_ENABLE_PRESTO_3PART_NAMES=true
         db2set DB2_WORKLOAD=ANALYTICS
         db2set DB2_REDUCED_OPTIMIZATION="EGAD 0,STARJN_CARD ON 1"
         db2set DB2_EXTENDED_OPTIMIZATION="REDSCANELIM_UCP ON,PCD ON,EXP_GRPSETS_BYREPL EAGGENF,MRG_DISJ_SCALARSQ_CASE ON,JFR ON,COLJOIN 1,PSQTGU ON,DISTINCT_ON_NULLARM_OF_OJ ON,EXP_GRPSETS_SIMPL_GBY_EXPR ON,EXP_GRPSETS_WITH_OLAP ON,ENFD2GBCSEIN ON"
         db2set DB2_SELECTIVITY=ALL
         db2set DB2_CORRELATED_PREDICATES="UNIQUE_KEY_JOIN_ADJUST ON"
         db2set DB2_OPTIMIZER_MODIFIERS="RSTFEXSTS ON,OJSJTE ON,CSE2OLAP ON,FJFR ON,DERSJF ON,D2GB4ED ON,GBSJFD ON"
         db2set DB2_UNION_OPTIMIZATION="OJ_UA_JPPD=ON"
          ```
         {: codeblock}

   b. OAAS db configuration settings

      i. Run the following command to update configuration as follows if it is not updated:

         ```bash
         db2 get db cfg
         db2 update db cfg for OAAS using LARGE_AGGREGATION NO
         ```
         {: codeblock}

      ii. Run the following command to restart:

         ```bash
         bigsql stop
         bigsql start
         bigsql status
         ```
         {: codeblock}
