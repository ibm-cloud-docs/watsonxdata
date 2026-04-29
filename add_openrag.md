---

copyright:
  years: 2026
lastupdated: "2026-04-29"

keywords: lakehouse, openrag, opensearch, watsonx.data, infrastructure manager, add component

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Adding an OpenRAG service (Private preview)
{: #add_openrag}

OpenRAG enables retrieval-augmented generation (RAG) workflows in {{site.data.keyword.lakehouse_full}} by using OpenSearch as the required search backend.
{: shortdesc}

Complete the following steps to add an OpenRAG service:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure Manager**.
1. In the **Services** section, select **OpenRAG** and click **Next**.

   The OpenRAG tile is displayed only if IBM enabled the private preview on your cluster.
   {: note}

1. In the **Add component - OpenRAG** window, provide the following details:

   - Select the service. For example, **OpenRAG**.
   - Select the suitable size. For example, **Starter**.

1. Click **Create**.

When the service is created, the console provisions OpenSearch first and then provisions OpenRAG by using the OpenSearch connection details.

The OpenRAG and OpenSearch services are displayed on the **Infrastructure Manager** page after provisioning is complete.
