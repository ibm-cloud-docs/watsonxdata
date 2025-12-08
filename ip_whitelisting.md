---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-08"

keywords: access, access control, access management

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

# Securing UI Access with IP-Based Controls
{: #access_rest}

This topic explains how to configure trusted IP addresses for UI access, allowing administrators to define which IP address can interact with specific user interface components. By implementing IP-based access controls, you can add an extra layer of protection, ensuring that only traffic from approved IP ranges can access {{site.data.keyword.lakehouse_short}}. For more information, see [What are context-based restrictions?](https://cloud.ibm.com/docs/account?topic=account-context-restrictions-whatis).
{: shortdesc}

## Before you begin
{: #access_bfb}

To configure trusted IP addresses for UI access, you must have Administrator privileges for the account.


## Configuring trusted IP access
{: #level_ipaddrs}

1. Sign in to IBM Cloud. Log in to your IBM Cloud account.

2. From the IBM Cloud Console, navigate to **Manage > Context-based restrictions**.

3. From the Navigation pane, click **Rules**.

4. Click **Create+**. The **New rule** page opens. Select {{site.data.keyword.lakehouse_short}} service from the list.

5. Click **Next**. Select all **APIs**.

6. Click **Next**. From **Resources**, select **Specific resource** option and choose {{site.data.keyword.lakehouse_short}}. You can review the selection.

7. Click **Continue**. From the **Network zones**, click **Create** and provide the list of IP addresses in the **Allowed IP addresses** field.

8. From the **Reference a service** section, select {{site.data.keyword.lakehouse_short}} as the service. Click **Continue**.
   The rule is created successfully.

   For more information, see [Creating context-based restrictions](https://cloud.ibm.com/docs/account?group=controlling-context-based-restrictions) and [Enforcing context-based restrictions](https://cloud.ibm.com/docs/account?topic=account-context-restrictions-create&interface=ui).


## Limitation
{: #limit_cbr}

CBR does not work for account-scoped lite instances.
