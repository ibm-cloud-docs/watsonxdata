---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-08"

keywords: lakehouse, engine, watsonx.data
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

# Provisioning a serverless Spark engine for Lite plan
{: #serv_spl_engine}


You can add serverless Spark engine for {{site.data.keyword.lakehouse_full}} Lite plan instance. Native serverless Spark engine is a compute engine that resides within IBM® watsonx.data.
{: shortdesc}

To add a Spark engine, complete the following steps.

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To add a Spark engine, click **Add component** and click **Next**.

5. In the **Add component** page, from the **Engines** section, select **IBM Spark**.

6. In the **Add component - IBM Spark** page, configure the following details:

      a. In the **Add component - IBM Spark** window, enter the **Display name** for your Spark engine.

      b. The **Registration mode** is by default **Create a native Spark engine**.


      c. Configure the following details:

      | Field | Description |
      | --- | --- |
      | Default Spark version | Select the Spark runtime version that must be considered for processing the applications. For supported Spark versions, see [Supported Spark version](/docs/watsonxdata?topic=watsonxdata-wxd-ae_limits#cpu-mem-spk_versn).\n Lite version of {{site.data.keyword.lakehouse_short}} does not support Spark version 4.0. |
      | Engine home bucket | Select the registered Cloud Object Storage bucket from the list to store the Spark events and logs that are generated while running spark applications. \n [Note]{: tag-purple} Make sure you do not select the IBM-managed bucket as Spark Engine home. If you select an IBM-managed bucket, you cannot access it to view the logs. \n For more information, see [Before you begin]({{site.data.keyword.ref-prov_nspark-link}}#prereq_nspark_prov).|
      |Instance resource quota| Displays the memory limit of the Spark engine. For Lite plan, it will be 8 vCPU and 32 GB. You cannot modify the value.   |
      |Associated catalogs (optional)| Select the catalogs that must be associated with the engine.   |
      {: caption="Provisioning Spark engine" caption-side="bottom"}


6. Click **Create**. The engine is provisioned and is displayed in the **Infrastructure Manager** page.


## T-shirt sizes for Serverless Spark
{: #tshirt_spk_engine}

For Lite plan, the default instance resource quota is  8 vCPU and 32 GB cpu memory. The {{site.data.keyword.lakehouse_short}} serverless Spark allows only the following pre-defined Spark driver and executor vCPU and memory combinations (T-shirt sizes) while submitting spark runtimes.

The following table shows the supported vCPU to memory size combinations.

| 1 : 2 ratio | 1 : 4 ratio | 1 : 8 ratio |
| ------------|-------------|-------------|
| 1 vCPU x 2 GB | 1 vCPU x 4 GB | 1 vCPU x 8 GB |
| 2 vCPU x 4 GB | 2 vCPU x 8 GB | 2 vCPU x 16 GB |
| 3 vCPU x 6 GB | 3 vCPU x 12 GB | 3 vCPU x 24 GB |
| 4 vCPU x 8 GB | 4 vCPU x 16 GB | NA  |
{: caption="Supported vCPU to memory size combinations" caption-side="top"}


You can view the CPU and memory usage in percentage from the Spark details page. For viewing the details, go to **Infrastructure Manager** > click on the Spark engine > click **Details** tab.
{: important}
