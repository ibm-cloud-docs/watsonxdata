---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-23"

keywords: lakehouse, watsonx data, roles, access
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

# Managing user access
{: #manage_access}

Security in {{site.data.keyword.lakehouse_full}} is based on roles. A role is a group of permissions that control the actions you can perform in {{site.data.keyword.lakehouse_short}}. To perform certain actions and manage specific sessions in {{site.data.keyword.lakehouse_short}}, the user must also have the appropriate authorization.
{: shortdesc}

Authorization is granted by assigning a specific role to the user account. Use the Role Based Access Control feature in {{site.data.keyword.lakehouse_short}} to grant users the access privileges they require for their role.

Access to provision IBM Cloud resources is governed by using [IAM access](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui). You must have **Administrator** privileges to access the resource group in which you need to create the resources.
{: note}

To manage access, complete the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Access control**.
   Under the **Infrastructure** tab, the different components (Engine, Catalog, Storage, and Database) are displayed in the table.

1. Click the overflow icon in the components row and then click **Manage access**. Alternatively, you can click the **Display name** of the component.
   The selected component page opens.

1. Under the **Access control** tab, click **Add access**.

1. In the **Grant access to users and user groups** window, provide the following details.

   | Field | Description |
   |--------------------------|----------------|
   | Name | You can select individual users or a user group.|
   | Role | Select the role from the drop-down list. You can assign roles based on the component type. For more information, see [Roles and privileges.]({{site.data.keyword.ref-role_priv-link}}){: external} |
   {: caption="Table 1. Add user" caption-side="bottom"}

   

1. Click **Add**. The user is added and assigned the role.

1. To change the role that is assigned to a user, complete the following steps:

   1. Under the **Infrastructure** tab, click the **Display name** of the component in the table.

      The **Access control** tab for selected component opens.

   1. Click the overflow menu for the selected user and then select **Change role**.

   1. In the **Change role** window, select the role from the drop-down list.

   1. Click **Save**.

1. To remove a user for a component, complete the following steps:

   1. Under the **Infrastructure** tab, click the **Display name** of the component in the table.

      The **Access control** tab for the selected component opens.

   1. Click the overflow menu for the selected user and then select **Remove**.

   1. In the **Confirm removal** window, click **Remove**.

      The user remains in the **Access control** tab after removing from {{site.data.keyword.Bluemix_notm}} or Cloud Pak for Data. You must remove the user manually from the **Access control** tab. You might see the user in the **Access control** tab of the engine after confirming the removal. It takes up to 20 minutes for the access revoke to be effective for the user and disappear from the tab.
      {: note}
