---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-29"

keywords: lakehouse, watsonx.data, query optimizer, uninstall

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

# Managing user settings in {{site.data.keyword.lakehouse_short}}: Session timeout, Query timeout, and Login message settings
{: #idle_session_timeout}

This topic outlines the steps to configure a `Session timeout`, set a `Query timeout`, and define a `Login message` in {{site.data.keyword.lakehouse_short}}.

**Session timeout:** Ends a user session automatically after a specified period of inactivity.

**Query Timeout:** Terminates all queries in a user session once they exceed the maximum execution time set by the user. If a `client timeout` is also configured, the system stops query execution when a network disruption or server-side change occurs.

**Login message:** You can set a login message.

## Procedure
{: #idle_session}

To manage user settings, complete the following steps:

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **User settings** tile. Or click **Profile** and click **Preference Settings**.
1. To set **Session timeout**, complete the following steps:
   1. Click **Edit**.
   1. Set the desired timeout duration for idle session timout and click **Save**.

      The default idle session timeout is set to 15 minutes. You can configure the timeout duration, with a minimum of 2 minutes and a maximum of 120 minutes.
      {: note}

1. To set **Query timeout**, complete the following steps:
   1. Enter **Maximum query execution time** and **Query client timeout**. If you have not configured the **Maximum Query Execution Time** and **Query Client Timeout**, the system sets the following default backend values:
   * `Maximum query execution time` = 1 hour
   * `Query Client Timeout` = 15 minutes

      This feature works only with Presto (Java) and Presto (C++) engines that are currently running. When you enable it, the system restarts both engines. The Lite Presto does not support this feature.
      {: note}

1. To set a **Login message**, complete the following steps:
   1. Click **Edit**.
   1. Click the toggle switch to enable the login message.
   1. Enter the title and the message.
   1. Click **Save**.
