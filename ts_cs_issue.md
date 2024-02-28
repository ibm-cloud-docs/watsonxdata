---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

keywords: watsonxdata, troubleshoot, case sensitivity

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

# Case-sensitive search configuration with Presto
{: #ts_cs}

When you deal with character data, case sensitivity is important when you search for specific matches or patterns. However, not all databases and query engines behave in the same way. Some are case-insensitive by default, while others are not. The case-sensitive search can lead to unexpected results if the case of the data is not considered.
{: shortdesc}
