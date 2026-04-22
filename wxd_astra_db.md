---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-22"

keywords: lakehouse, astra db, watsonx.data, pricing

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

# Astra DB pricing
{: #wxd_astra_db_pp}

Select the appropriate pricing plan for your Astra DB deployment by reviewing the tables provided in this page.

## Astra DB billable meters and measures
{: #wxd_adb_billable_meters}

The following table provides a current list of Astra DB billable meters and their measures. A billable meter is any metered metric on the Astra platform that results in a billable event which deducts the corresponding number of Resource Units (RU) from the customer's total credit balance or gets applied to a credit balance due for pay-as-you-go customers.

| Product or Service | Meter | Measure |
| --- | --- | --- |
| Astra DB on-demand: Reads | Number of writes | Per 1 million |
| Astra DB on-demand: Writes | Number of reads | Per 1 million |
| Astra DB on-demand: Vector dimension reads | Number of reads | Per 1 million |
| Astra DB on-demand: Vector dimension writes | Number of reads | Per 1 million |
| Astra DB provisioned capacity units all types | Number of hours | Per hour |
| Astra DB storage: All types | GB stored | Maximum per month |
| Astra DB data transfer: All types | GB transferred | Total GB transferred |
| Astra DB private link: Active | Hours | Per hour |
| Astra DB private link: Ingress | GB transferred | Total GB transferred |
| Astra DB private link: Egress | GB transferred | Total GB transferred |
{: caption="Current Astra DB billable meters and measures" caption-side="top"}

## Astra DB rates
{: #wxd_adb_rates}

The following tables provide current Astra DB rates. All costs are reflected in Resource Units (RU).

### On-demand pricing (per million reads)
{: #wxd_adb_ondemand_reads}

| Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- |
| AWS | North America | 0.62 | 0.69 | |
| AWS | EMEA | 0.68 | 0.75 | 0.79 |
| AWS | SA | | | 0.96 |
| AWS | APAC | 0.61 | 0.83 | |
| AZURE | North America | 0.66 | 0.73 | |
| AZURE | EMEA | 0.69 | 0.78 | |
| AZURE | APAC | 0.72 | 0.83 | |
| AZURE | SA | | | 0.95 |
| GCP | North America | 0.60 | 0.70 | |
| GCP | APAC | 0.65 | 0.77 | |
| GCP | EMEA | 0.67 | 0.70 | |
{: caption="On-demand pricing (per million reads)" caption-side="top"}

### On-demand pricing (per million writes)
{: #wxd_adb_ondemand_writes}

| Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- |
| AWS | North America | 1.04 | 1.14 | |
| AWS | EMEA | 1.23 | 1.31 | |
| AWS | SA | | | 1.72 |
| AWS | APAC | 1.06 | 1.29 | |
| AZURE | North America | 1.12 | 1.22 | |
| AZURE | EMEA | 1.17 | 1.25 | |
| AZURE | APAC | 1.20 | 1.30 | |
| AZURE | SA | | | 1.52 |
| GCP | North America | 1.02 | 1.12 | |
| GCP | APAC | 1.09 | 1.23 | |
| GCP | EMEA | 1.14 | 1.28 | |
{: caption="On-demand pricing (per million writes)" caption-side="top"}

### Vector: On-demand pricing (per million reads)
{: #wxd_adb_vector_reads}

| Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- |
| AWS | North America | 0.70 | | |
| AWS | EMEA | 0.70 | 0.70 | |
| AWS | SA | | | 0.90 |
| AWS | APAC | 0.60 | 0.70 | |
| AZURE | North America | 0.70 | | |
| AZURE | EMEA | 0.70 | 0.70 | |
| AZURE | APAC | 0.70 | 0.70 | |
| AZURE | SA | | | 0.90 |
| GCP | North America | 0.70 | 0.70 | |
| GCP | APAC | 0.70 | | |
| GCP | EMEA | 0.70 | 0.70 | |
{: caption="Vector: On-demand pricing (per million reads)" caption-side="top"}

### Vector: On-demand pricing (per million writes)
{: #wxd_adb_vector_writes}

| Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- |
| AWS | North America | 0.70 | | |
| AWS | EMEA | 0.70 | 0.70 | |
| AWS | SA | | | 0.90 |
| AWS | APAC | 0.60 | 0.70 | |
| AZURE | North America | 0.70 | | |
| AZURE | EMEA | 0.70 | 0.70 | |
| AZURE | APAC | 0.70 | 0.70 | |
| AZURE | SA | | | 0.90 |
| GCP | North America | 0.70 | 0.70 | |
| GCP | APAC | 0.70 | 0.70 | |
| GCP | EMEA | 0.70 | 0.70 | |
{: caption="Vector: On-demand pricing (per million writes)" caption-side="top"}

### Reserved capacity units (with 12 month commit) - Shared or Multi-tenant
{: #wxd_adb_rcu_shared}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Reserved Capacity Unit (RCU) | AWS | APAC | 8.01 | 10.06 | |
| Reserved Capacity Unit (RCU) | AWS | EMEA | 9.20 | | |
| Reserved Capacity Unit (RCU) | AWS | North America | 9.28 | | |
| Reserved Capacity Unit (RCU) | AWS | SA | | | 12.21 |
| Reserved Capacity Unit (RCU) | AZURE | APAC | 9.43 | 10.99 | |
| Reserved Capacity Unit (RCU) | AZURE | EMEA | 9.94 | 11.39 | |
| Reserved Capacity Unit (RCU) | AZURE | North America | 9.02 | 9.86 | |
| Reserved Capacity Unit (RCU) | AZURE | SA | | | 13.44 |
| Reserved Capacity Unit (RCU) | GCP | APAC | 9.93 | 11.28 | |
| Reserved Capacity Unit (RCU) | GCP | EMEA | 9.39 | 10.57 | |
{: caption="Reserved capacity units (with 12 month commit) - SharedorMulti-tenant" caption-side="top"}

### Cache optimization add-on for shared reserved capacity units (RCU)
{: #wxd_adb_cache_shared_rcu}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Cache Optimization Add-On | AWS | APAC | 4.83 | 3.57 | |
| Cache Optimization Add-On | AWS | EMEA | 3.66 | | |
| Cache Optimization Add-On | AWS | North America | 3.23 | | |
| Cache Optimization Add-On | AWS | SA | | | 5.18 |
| Cache Optimization Add-On | AZURE | APAC | 4.60 | 4.66 | |
| Cache Optimization Add-On | AZURE | EMEA | 4.56 | 5.49 | |
| Cache Optimization Add-On | AZURE | North America | 4.08 | 4.48 | |
| Cache Optimization Add-On | AZURE | SA | | | 6.27 |
| Cache Optimization Add-On | GCP | APAC | 3.86 | 4.61 | |
| Cache Optimization Add-On | GCP | EMEA | 3.70 | 4.25 | |
| Cache Optimization Add-On | GCP | NA | 3.44 | | |
{: caption="Cache optimization add-on for shared reserved capacity units (RCU)" caption-side="top"}

### Reserved capacity units (with 12 month commit) - Dedicated or Single-tenant
{: #wxd_adb_rcu_dedicated}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Reserved Capacity Unit (RCU) | AWS | APAC | 9.61 | 12.07 | |
| Reserved Capacity Unit (RCU) | AWS | EMEA | 11.04 | | |
| Reserved Capacity Unit (RCU) | AWS | North America | 9.94 | | |
| Reserved Capacity Unit (RCU) | AWS | SA | | | 14.65 |
| Reserved Capacity Unit (RCU) | AZURE | APAC | 11.32 | 13.18 | |
| Reserved Capacity Unit (RCU) | AZURE | EMEA | 11.93 | 13.67 | |
| Reserved Capacity Unit (RCU) | AZURE | North America | 10.82 | 11.83 | |
| Reserved Capacity Unit (RCU) | AZURE | SA | | | 16.13 |
| Reserved Capacity Unit (RCU) | GCP | APAC | 11.91 | 13.54 | |
| Reserved Capacity Unit (RCU) | GCP | EMEA | 11.27 | 12.68 | |
| Reserved Capacity Unit (RCU) | GCP | NA | 10.52 | | |
{: caption="Reserved capacity units (with 12 month commit) - Dedicated or Single-tenant" caption-side="top"}

### Cache optimization add-on for dedicated reserved capacity units (RCU)
{: #wxd_adb_cache_dedicated_rcu}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Cache Optimization Add-On | AWS | APAC | 8.70 | 6.42 | |
| Cache Optimization Add-On | AWS | EMEA | 6.58 | | |
| Cache Optimization Add-On | AWS | North America | 5.82 | | |
| Cache Optimization Add-On | AWS | SA | | | 9.33 |
| Cache Optimization Add-On | AZURE | APAC | 8.28 | 8.39 | |
| Cache Optimization Add-On | AZURE | EMEA | 8.20 | 9.87 | |
| Cache Optimization Add-On | AZURE | North America | 7.35 | 8.07 | |
| Cache Optimization Add-On | AZURE | SA | | | 11.29 |
| Cache Optimization Add-On | GCP | APAC | 6.96 | 8.29 | |
| Cache Optimization Add-On | GCP | EMEA | 6.65 | 7.66 | |
| Cache Optimization Add-On | GCP | NA | 6.20 | | |
{: caption="Cache optimization add-on for dedicated reserved capacity units (RCU)" caption-side="top"}

### Hourly capacity units (No 12 month commit) - Shared or Multi-tenant
{: #wxd_adb_hcu_shared}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Hourly Capacity Unit (HCU) | AWS | APAC | 12.01 | 15.09 | |
| Hourly Capacity Unit (HCU) | AWS | EMEA | 13.79 | | |
| Hourly Capacity Unit (HCU) | AWS | North America | 12.42 | | |
| Hourly Capacity Unit (HCU) | AWS | SA | | | 18.31 |
| Hourly Capacity Unit (HCU) | AZURE | APAC | 14.14 | 16.48 | |
| Hourly Capacity Unit (HCU) | AZURE | EMEA | 14.91 | 17.08 | |
| Hourly Capacity Unit (HCU) | AZURE | North America | 13.52 | 14.78 | |
| Hourly Capacity Unit (HCU) | AZURE | SA | | | 20.16 |
| Hourly Capacity Unit (HCU) | GCP | APAC | 14.89 | 16.92 | |
| Hourly Capacity Unit (HCU) | GCP | EMEA | 14.09 | 15.85 | |
| Hourly Capacity Unit (HCU) | GCP | NA | 13.15 | | |
{: caption="Hourly capacity units (No 12 month commit) - Shared or Multi-tenant" caption-side="top"}

### Cache optimization add-on for shared hourly capacity units (HCU)
{: #wxd_adb_cache_shared_hcu}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Cache Optimization Add-On | AWS | APAC | 7.25 | 5.24 | |
| Cache Optimization Add-On | AWS | EMEA | 5.49 | | |
| Cache Optimization Add-On | AWS | North America | 4.85 | | |
| Cache Optimization Add-On | AWS | SA | | | 7.78 |
| Cache Optimization Add-On | AZURE | APAC | 6.90 | 6.99 | |
| Cache Optimization Add-On | AZURE | EMEA | 6.83 | 8.23 | |
| Cache Optimization Add-On | AZURE | North America | 6.12 | 6.72 | |
| Cache Optimization Add-On | AZURE | SA | | | 9.41 |
| Cache Optimization Add-On | GCP | APAC | 5.80 | 6.91 | |
| Cache Optimization Add-On | GCP | EMEA | 5.54 | 6.38 | |
| Cache Optimization Add-On | GCP | NA | 5.16 | | |
{: caption="Cache optimization add-on for shared hourly capacity units (HCU)" caption-side="top"}

### Hourly capacity units (No 12 month commit) - Dedicated or Single-tenant
{: #wxd_adb_hcu_dedicated}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Hourly Capacity Unit (HCU) | AWS | APAC | 14.42 | 18.11 | |
| Hourly Capacity Unit (HCU) | AWS | EMEA | 16.55 | | |
| Hourly Capacity Unit (HCU) | AWS | North America | 14.91 | | |
| Hourly Capacity Unit (HCU) | AWS | SA | | | 21.97 |
| Hourly Capacity Unit (HCU) | AZURE | APAC | 16.97 | 19.78 | |
| Hourly Capacity Unit (HCU) | AZURE | EMEA | 17.89 | 20.50 | |
| Hourly Capacity Unit (HCU) | AZURE | North America | 16.23 | 17.74 | |
| Hourly Capacity Unit (HCU) | AZURE | SA | | | 24.20 |
| Hourly Capacity Unit (HCU) | GCP | APAC | 17.87 | 20.31 | |
| Hourly Capacity Unit (HCU) | GCP | EMEA | 16.91 | 19.03 | |
| Hourly Capacity Unit (HCU) | GCP | NA | 15.78 | | |
{: caption="Hourly capacity units (No 12 month commit) - Dedicated or Single-tenant" caption-side="top"}

### Cache optimization add-on for dedicated hourly capacity units (HCU)
{: #wxd_adb_cache_dedicated_hcu}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Cache Optimization Add-On | AWS | APAC | 8.70 | 6.42 | |
| Cache Optimization Add-On | AWS | EMEA | 6.58 | 7.35 | 6.54 |
| Cache Optimization Add-On | AWS | North America | 5.82 | 5.87 | |
| Cache Optimization Add-On | AWS | SA | | | 9.33 |
| Cache Optimization Add-On | AZURE | APAC | 8.28 | 8.39 | |
| Cache Optimization Add-On | AZURE | EMEA | 8.20 | 9.87 | 11.93 |
| Cache Optimization Add-On | AZURE | North America | 7.35 | 8.07 | |
| Cache Optimization Add-On | AZURE | SA | | | 11.29 |
| Cache Optimization Add-On | GCP | APAC | 6.96 | 8.29 | |
| Cache Optimization Add-On | GCP | EMEA | 6.65 | 7.66 | 9.02 |
| Cache Optimization Add-On | GCP | NA | 6.20 | 7.06 | |
| Cache Optimization Add-On | GCP | SA | | | 6.44 |
{: caption="Cache optimization add-on for dedicated hourly capacity units (HCU)" caption-side="top"}

### Storage pricing - RU cost per GB stored
{: #wxd_adb_storage}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Data Storage | AWS | APAC | 0.39 | 0.45 | |
| Data Storage | AWS | EMEA | 0.41 | 0.43 | 0.45 |
| Data Storage | AWS | North America | 0.42 | 0.42 | |
| Data Storage | AWS | SA | | | 0.68 |
| Data Storage | AZURE | APAC | 0.45 | 0.45 | |
| Data Storage | AZURE | EMEA | 0.44 | 0.44 | |
| Data Storage | AZURE | North America | 0.42 | 0.42 | |
| Data Storage | AZURE | SA | | | 0.63 |
| Data Storage | GCP | APAC | 0.45 | 0.47 | |
| Data Storage | GCP | EMEA | 0.44 | 0.46 | |
| Data Storage | GCP | NA | 0.42 | 0.42 | |
{: caption="Storage pricing - RU cost per GB stored" caption-side="top"}

### Data transfer pricing - Same region
{: #wxd_adb_transfer_same}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Data Transfer - Same Region | AWS | APAC | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AWS | EMEA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AWS | North America | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AWS | SA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AZURE | APAC | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AZURE | EMEA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AZURE | North America | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | AZURE | SA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | GCP | APAC | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | GCP | EMEA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | GCP | NA | 0.23 | 0.23 | 0.23 |
| Data Transfer - Same Region | GCP | SA | 0.23 | 0.23 | 0.39 |
{: caption="Data transfer pricing - Same region" caption-side="top"}

### Data transfer pricing - Within cloud provider network
{: #wxd_adb_transfer_network}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Data Transfer - Within Cloud Provider | AWS | APAC | 0.19 | 0.22 | |
| Data Transfer - Within Cloud Provider | AWS | EMEA | 0.08 | 0.08 | 0.33 |
| Data Transfer - Within Cloud Provider | AWS | North America | 0.08 | 0.08 | |
| Data Transfer - Within Cloud Provider | AWS | SA | | | 0.35 |
| Data Transfer - Within Cloud Provider | AZURE | APAC | 0.15 | 0.16 | |
| Data Transfer - Within Cloud Provider | AZURE | EMEA | 0.05 | 0.05 | |
| Data Transfer - Within Cloud Provider | AZURE | North America | 0.05 | 0.05 | |
| Data Transfer - Within Cloud Provider | AZURE | SA | | | 0.31 |
| Data Transfer - Within Cloud Provider | GCP | APAC | 0.14 | 0.18 | |
| Data Transfer - Within Cloud Provider | GCP | EMEA | 0.05 | 0.05 | |
| Data Transfer - Within Cloud Provider | GCP | NA | 0.05 | 0.05 | |
{: caption="Data transfer pricing - Within cloud provider network" caption-side="top"}

### Data transfer pricing - Internet
{: #wxd_adb_transfer_internet}

| Type | Provider | Region | Standard | Premium | Premium Plus |
| --- | --- | --- | --- | --- | --- |
| Data Transfer - Internet | AWS | APAC | 0.22 | 0.26 | |
| Data Transfer - Internet | AWS | EMEA | 0.18 | 0.18 | 0.30 |
| Data Transfer - Internet | AWS | North America | 0.18 | 0.18 | |
| Data Transfer - Internet | AWS | SA | | | 0.35 |
| Data Transfer - Internet | AZURE | APAC | 0.26 | 0.26 | |
| Data Transfer - Internet | AZURE | EMEA | 0.22 | 0.22 | |
| Data Transfer - Internet | AZURE | North America | 0.19 | 0.19 | |
| Data Transfer - Internet | AZURE | SA | | | 0.31 |
| Data Transfer - Internet | GCP | APAC | 0.28 | 0.38 | |
| Data Transfer - Internet | GCP | EMEA | 0.24 | 0.25 | |
| Data Transfer - Internet | GCP | NA | 0.23 | 0.23 | |
{: caption="Data transfer pricing - Internet" caption-side="top"}

### Private link pricing
{: #wxd_adb_private_link}

The following private link pricing applies to all available providers and regions:

| Type | Rate |
| --- | --- |
| Private link active | 1.20 RU per hour |
| Private link ingress | 1.20 RU per GB |
| Private link egress | 1.20 RU per GB |
{: caption="Private link pricing" caption-side="top"}
