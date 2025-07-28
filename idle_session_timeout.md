---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-28"

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

This topic outlines the steps to manage user settings in {{site.data.keyword.lakehouse_short}}.

## Procedure
{: #idle_session}

To manage user settings, complete the follwoing steps:

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **User settings** tile. Or click **Profile** and click **Preference Settings**.
1. To set **Session timeout**, complete the follwoing steps:
   1. Click **Edit**.
   1. Set the desired timeout duration for idle session timout and click **Save**.

      The default idle session timeout is set to 15 minutes. You can configure the timeout duration, with a minimum of 2 minutes and a maximum of 120 minutes.
      {: note}

1. To set **Query timeout**, complete the follwoing steps:
   1. Enter **Maximum query execution time** and **Query client timeout**.

      If no supporting engines are available, the system disables the query timeout setting.
      {: note}

1. To set a **Login message**, complete the following steps:
   1. Click **Edit**.
   1. Click the toggle switch to enable the login message.
   1. Enter the title and the message.
   1. Click **Save**.
