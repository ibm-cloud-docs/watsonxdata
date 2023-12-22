---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

keywords: lakehouse, access, data, policy, watsonx data

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


# Managing data policy rules
{: #data_policy}

Protecting access to data is a critical requirement for many enterprises. To ensure that your data is protected from unauthorized access, {{site.data.keyword.lakehouse_full}} can manage access controls for data. A user with admin privileges on the data can create access policies to define, extend, limit and deny, by using the data security solution that is provided by {{site.data.keyword.lakehouse_short}}.
{: shortdesc}

To maintain data security, you can create access policies for the following at the data level:

1. Schemas, tables, and columns.
2. Users or user groups.
3. Actions.

## Create Access control policies
{: #crea_acc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Access control**.
1. Select **Policies** from the **Access control** page, click **Add policy**. **Create access control policy** page opens.
1. In the **Basics** page, enter a policy name, policy description and select the policy status after creation. Click **Next**.
1. In the **Data** page, select a catalog and choose a single or all schema, table, or column where you want to add the data policy.
1. Click **Next** to add rules.
1. In the **Rules** page, click **Add rule**.
1. Select the rule type, user actions, users or groups and click **Add** to add the rule.
1. Click **Review** to see the rule.
1. Click **Save** to save the policy.
