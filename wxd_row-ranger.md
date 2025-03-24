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

# Adding row-level filtering policy
{: #row_ranger}

Row-level filtering allows users to access a subset of rows in a table.
{: shortdesc}


## Before you begin
{: #row_ranger_2}

Ensure you have the following details:

* IBM watsonx.data instance.
* Apache Ranger is provisioned.
* Enable the Apache Ranger policy in watsonx.data. For more information, see [Enabling Apache Ranger policy for resources](/docs/watsonxdata?topic=watsonxdata-ranger_1){: external}. .


## Procedure
{: #row_ranger_3}

Complete the following steps.


1. Log in to Apache Ranger by using the username and password.

    a. Go to **Service Manager** > **`service_name` policies** page to add a row level filter policy.

    b. In the **Policy Details** section, provide the policy details like name, description.

    c. In the **Resources** section, select the catalog, schema, and table for which the policy is applicable.

    d. In the **Row Filter Conditions** section, select the user (example, **User1**), set the **Permissions** to **Select** and enter the **Row Level Filter** (example, c1=1).

    e. Click **Save**.

2. Complete the following steps to verify access control:


    a. Log in to watsonx.data instance as User1.

    b. From the navigation menu, click **Query workspace**.

    c. Run a simple query to access the table again, now **User1** can only see rows with column c1 equal to 1 in the result.
