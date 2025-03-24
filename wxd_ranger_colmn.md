---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

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

# Adding column masking policy
{: #colmn_ranger_1}

IBM watsonx.data now supports Apache Ranger policies to allow comprehensive data security on integrating with multiple governance tools and engines.
{: shortdesc}


## Before you begin
{: #colmn_ranger_2}

Ensure you have the following details:

* IBM watsonx.data instance.
* Apache Ranger is provisioned.
* Enable the Apache Ranger policy in watsonx.data. For more information, see [Enabling Apache Ranger policy for resources](/docs/watsonxdata?topic=watsonxdata-ranger_1){: external}. .


## Procedure
{: #colmn_ranger_3}

1. Complete the following steps.


    a. Log in to **Apache Ranger** by using the username and password.

    b. Go to **Service Manager** > **`service_name` policies** page to add a masking policy.

    c. In the **Policy Details** section, provide the policy details like name, description.

    d. In the **Resources** section, select the catalog, schema, table, and column for which the policy is applicable.

    e. In the **Masking Conditions** section, select the user (example, **User1**), set the **Permissions** to **Select**, set the Select Masking Option to Custom and enter the masked value as **xxx**.

    f. Click **Save**.

2. Complete the following steps to verify access control:


    a. Log in to watsonx.data instance as User1.

    b. From the navigation menu, click **Query workspace**.

    c. Run a simple query to access the table again, now User1 view see the sensitive data in masked format (xxx) in the target column in the result.
