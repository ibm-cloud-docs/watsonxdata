---

copyright:
  years: 2024
lastupdated: "2024-09-13"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring Spark application runs by using Databand
{: #mntr_dband}

Databand integration with Spark enhances monitoring capabilities by providing insights that extend beyond Spark UI and Spark History.

Databand improves Spark application monitoring by the following:

- **Advanced monitoring**: Databand’s task annotations enable you to tag and track crucial stages of your Spark application, offering a more meaningful level of monitoring compared to Spark jobs, stages, or tasks.
- **Dataset tracking**: Databand monitors the datasets that are accessed and modified during your Spark application run, providing enhanced visibility into your data flows.
- **Custom alerts**: You can configure alerts for specific stages of your application or track key dataset metrics, allowing you to identify and address potential issues early.

To get started with Databand, you must have an active Databand subscription. You can obtain this by either requesting a Databand cloud application (SaaS) instance, which is deployed by the Databand team, or by opting for a self-hosted (on-premises) installation. For integrating databand with your watsonx.data instance, you must have the following credentials:

- **Environment address**: The URL for your Databand environment (example: yourcompanyname.databand.ai).
- **Access token**: A Databand access token that is needed to connect to the environment. You can generate and manage tokens through the Databand UI as required. For more details, visit: [Managing personal access tokens](https://www.ibm.com/docs/en/dobd?topic=tokens-managing-personal-access).

## What to do next
{: #what_next}

- [Track Spark applications](watsonxdata?topic=watsonxdata-db_trk)
- [Invoke Spark Applications](watsonxdata?topic=watsonxdata-db_inv)
