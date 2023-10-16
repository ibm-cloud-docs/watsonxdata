---

copyright:
  years: 2022, 2023
lastupdated: "2023-10-11"

keywords: lakehouse

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


# Understanding your responsibilities when using {{site.data.keyword.lakehouse_short}}
{: #response}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.lakehouse_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix_short}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.Bluemix_short}} offerings](https://cloud.ibm.com/docs/overview?topic=overview-shared-responsibilities).
Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.lakehouse_short}}. For the overall terms of use, see [{{site.data.keyword.Bluemix_short}} Terms and Notices](https://cloud.ibm.com/docs/overview/terms-of-use?topic=overview-terms).
{: shortdesc}

## Incident and operations management
{: #incident}

Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.


| Task | IBM responsibilities |Your responsibilities |
|--------------------------|----------------|----------------|
| {{site.data.keyword.lakehouse_full}} instance administration| * Provide infrastructure operating system (OS), version, and security updates. \n * Clean up all instance resources. \n * Track hardware issues on running cluster.| * Create an instance using the provided API, CLI or console tools. \n * Delete a service instance using the provided API, CLI or console tools. \n * Customize a service instance using the provided API or CLI. \n * View or change the instance configuration using the provided API, CLI or console tools.|
|Application administration|Monitor {{site.data.keyword.lakehouse_short}} for any failures due to infrastructure provided by {{site.data.keyword.IBM_notm}}.|* Run {{site.data.keyword.lakehouse_short}} using the provided CLI, API or console tools. \n * Tune the {{site.data.keyword.lakehouse_short}} instance for your requirements using the provided CLI, API, or console tools.|
|Observability|* Provide Log Analysis to enable observability of your {{site.data.keyword.lakehouse_full}} service logs. \n * Provide integration with Activity Tracker to send {{site.data.keyword.lakehouse_full}} events for auditability.|* Set up Activity Tracker and send events to monitor the health of your {{site.data.keyword.lakehouse_full}} instances. \n * Set up and send logs to Log Analysis.|
{: caption="Table 1.Incident and operations management" caption-side="bottom"}

## Change management
{: #change_mgt}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

| Task | IBM responsibilities |Your responsibilities |
|--------------------------|----------------|----------------|
| Instance provisioning| * Order hardware (data plane in the IBM services account). \n * Open the {{site.data.keyword.lakehouse_short}} cluster to the internet (data plane in the IBM Services account). \n * Ensure network isolation of the {{site.data.keyword.lakehouse_short}} cluster nodes from other clusters (data plane in the IBM Services account). \n * Patch the cluster hosts (data plane in the IBM Services account). \n * Ensure safe erasure of data from removed node or deleted cluster nodes. \n * Delete hardware (data plane in the IBM Services account).| No change management responsibilities|
{: caption="Table 2.Change management" caption-side="bottom"}

## Identity and access management
{: #idnt_access_mgt}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

| Task | IBM responsibilities |Your responsibilities |
|--------------------------|----------------|----------------|
| Access control of the service instance through IAM| Verify the user's permissions on the service instance before allowing access.| Maintain responsibility for any service roles that you create for your instances.|
{: caption="Table 3.Identity and access management" caption-side="bottom"}

## Security and regulation compliance
{: #security_comp}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification.


| Task | IBM responsibilities |Your responsibilities |
|--------------------------|----------------|----------------|
| General| * Maintain controls commensurate to various industry compliance standards. \n * Monitor, isolate, and recover instances. \n * Monitor and report the health of instances in the various interfaces. \n * Secure cluster access through TLS/SSH (data plane in the IBM Services account). \n * Integrate {{site.data.keyword.lakehouse_short}} with IBM Cloud Identity and Access Management (IAM).| Set up and maintain security and regulation compliance for the {{site.data.keyword.lakehouse_short}} instances.|
{: caption="Table 4.Security and regulation compliance" caption-side="bottom"}

## Disaster recovery
{: #security_comp}


| Task | IBM responsibilities |Your responsibilities |
|--------------------------|----------------|----------------|
| General| * Restore or rebuild the provisioning environments in the affected regions. \n * Restore existing {{site.data.keyword.lakehouse_short}} instances, where possible. | * Track instance state. \n * Provision new {{site.data.keyword.lakehouse_short}} instances in alternatively available regions.\n * Ensure that the {{site.data.keyword.lakehouse_short}} instance is stateless by making sure that all data, metadata and applications reside outside of the cluster. This activity must be completed before disaster recovery can be initiated.\n * Provision a new service instance in an alternatively available region if the current instances can't be accessed.|
{: caption="Table 5.Disaster recovery" caption-side="bottom"}
