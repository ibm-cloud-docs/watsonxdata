---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing user access for Native Spark engine
{: #manage_user_access}

## Add a user
{: #add_user}

For information about resource-level permissions of various user roles, see [Managing roles and privileges](watsonxdata?topic=watsonxdata-role_priv#native_spark).
{: note}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Access control**.

   The **Infrastructure** tab shows the different components (Engine, Catalog, Bucket, and Database) in the table.
1. Click the overflow icon in a component's row and then click **Manage access**.

   Alternatively, you can click the **Display name** of the component. The component page opens.
1. Go to the **Access control** tab and click **Add access**.
1. In the **Add access** window, provide the following details.

| Field | Description |
|-------|-----------------|
| Name | Select individual users or a user group.|
| Role | Select the role from the drop-down list. You can assign roles based on the component type. For more information, see [Managing roles and privileges](watsonxdata?topic=watsonxdata-role_priv#native_spark).|
{: caption="Table 1. Add access" caption-side="bottom"}

1. Click **Add**. The user is added with the assigned role.

To remove a role, click the overflow menu for the selected user and then select Remove.
{: note}

## Change role of a user
{: #change_role}

To change the role that is assigned to a user, complete the following steps:

1. Under the **Infrastructure** tab, click the **Display name** of the component in the table.

   The **Access control** tab for selected component opens.
1. Click the overflow menu for the selected user and select **Change role**.
1. In the **Change role** window, select the role from the drop-down list.
1. Click **Save**.

## Remove a user
{: #cremove_user}

To remove a user from a component, complete the following steps:

1. Under the **Infrastructure** tab, click the **Display name** of the component in the table.
1. The **Access control** tab for the selected component opens.
1. Click the overflow menu for the selected user and then select **Remove**.
1. In the **Confirm removal** window, click **Remove**.
