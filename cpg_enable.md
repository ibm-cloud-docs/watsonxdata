---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-24"

keywords: watsonxdata, schema

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



# Enabling or disabling common policy gateway engines
{: #create_ebl_cpg}

The Common Policy Gateway (CPG) is a critical component in watsonx.data that serves as a centralized gateway for integrating multiple policy governance engines across diverse data sources.
{: shortdesc}

You can enable or disable CPG provisioning based on the specific requirement of a policy engine. If a policy engine—such as Ranger, or IKC is needed, CPG can be provisioned else you can disable it.

## Enabling CPG
{: #cpg_ebl}

1. Log in to the watsonx.data console.

1. From the navigation menu, select **Access control**. Click the **Integrations** tab.

1. Use the **External policy** toggle button to enable the Common Policy Gateway engine. A confirmation message opens. Click **Confirm** to proceed enabling the CPG feature. By default, the External policy toggle button will be in disabled state.

1. After you enable CPG, the **Integrate service** button is activated and ready for use.

1. Use the button **Integrate service** to enable the required policy engines such as IKC or Ranger.


## Disabling CPG
{: #cpg_dsbl}


1. Log in to the watsonx.data console.

1. From the navigation menu, select **Access control**. Click the **Integrations** tab.

1. To disable CPG, you must remove all the existing policy engines.

1. Select the policy engine. Click the overflow menu against the policy and select **Deactivate**. On confirming the updates, the policy will be deactivated.

1. Click the overflow menu against the policy and select **Delete**. On confirming the updates, the policy will be removed.

1. Use the External policy toggle button to disable the Common Policy Gateway engines. A confirmation message opens. Click **Confirm** to proceed disabling the CPG feature.
