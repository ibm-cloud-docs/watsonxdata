---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-22"

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

1. Data objects, such as schemas, tables, and columns.
2. Users or user groups.
3. Actions.

## Create Access control policies
{: #crea_acc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Access control**.
1. Select **Policies** from the **Access control** page, click **Add policy**. The **Create access control policy** page opens.
1. In the **Details** page, enter the following details and click **Next**:
   | Field | Description |
   | --- | --- |
   | Policy name | Enter a name. |
   | Policy description (Optional) | Give a brief description. |
   | Policy status after creation | Set the status to activate the policy at the time of creation or later. |
   {: caption="Table 1. Policy details" caption-side="bottom"}

1. In the **Data objects** page, select a resource from the drop-down list.

   You can select one of the following categories:
   - **Eligible catalogs**

     1. Select a catalog.
     1. Choose one, more than one, or all schemas.

        If you choose a single schema, you can select one, more than one, or all tables. If you choose more than one schema, you cannot select any tables. The policy applies to all tables within the schemas.
        {: note}

     1. Choose one, more than one, or all tables.

        If you choose a single table, you can select one, more than one, or all columns. If you choose more than one table, you cannot select any columns. The policy applies to all columns of the tables.
        {: note}

   - **Storage**

     1. Select a storage.
     1. Choose an object. Choose **Regular Expression** to enter the object path manually or **Explore object path** to search and select the object.

   - **Eligible services**

     1. Select a service.

        Currently, Milvus is the only service available. You can define policies to a Milvus service directly without selecting any databases. Select the service and proceed with step 6.
        {: note}

     1. Choose one, more than one, or all databases.
     1. Choose one, more than one, or all collections.

        If you choose a single database, you can select one, more than one, or all collections. If you choose more than one database, you cannot select any collections. The policy applies to all collections in the selected databases.
        {: note}

1. Click **Next**.
1. In the **Rules** page, click **Add rule** to go to the **Add rule** page.
1. Select the rule type **Allow** or **Deny**.
1. Select the actions on the data objects. The list of actions depend on the data object chosen in the earlier page. You can select one or more actions.
1. Choose if you want to grant access to individual users or a group of users from the **Users/groups** section.
1. Select a user or user group from the drop-down list.
1. Click **Add** to add the rule. You can add more rules or click **Review**, the **Summary** page opens.
1. In the **Summary** page:
   - You can review the policy.
   - Click **Back** to go to the previous page.
   - Click **Cancel** to cancel the process.
   - Click **Save** to save the policy.
