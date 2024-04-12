---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

# IBM Cloud IP address restriction
{: #ts_ip_restrict}

If you enable IP address restriction in {{site.data.keyword.cloud_notm}}, add the IP addresses that you use to access {{site.data.keyword.lakehouse_short}} to the allowed list in {{site.data.keyword.cloud_notm}}. Otherwise, the system denies access.
{: shortdesc}

## Procedure
{: #Procedure_ip}

1. Retrieve the IP address available in the regional Cloudflare trace page.

   **Trace page format:**

   ```bash
   https://<region>.lakehouse.cloud.ibm.com/cdn-cgi/trace
   ```
   {: codeblock}

   **For example:**

   ```bash
   https://eu-de.lakehouse.cloud.ibm.com/cdn-cgi/trace
   ```
   {: codeblock}

   **Output:**

   ```bash
   fl=374f35
   h=eu-de.lakehouse.cloud.ibm.com
   ip=171.76.80.113
   ts=1712133673.168
   visit_scheme=https
   uag=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
   colo=BLR
   sliver=010-tier3
   http=http/2
   loc=IN
   tls=TLSv1.3
   sni=plaintext
   warp=off
   gateway=off
   rbi=off
   kex=X25519
   ```
   {: screen}

1. Add the IP address that is retrieved from the trace page to the allowed IP address list and click **Save**.

   The IP address that is displayed with **Hint** might not match with the one available in the trace page. Add the value from the trace page instead of the value with **Hint**.
   {: note}

   To add multiple IP addresses in a range, use a CIDR block. For example, if you want to include all IP addresses between `171.76.80.0` and `171.76.80.255`, include the CIDR block `171.76.80.128/24`.

For more information, see [Allowing specific IP addresses for an account](https://cloud.ibm.com/docs/account?topic=account-ips&interface=ui#ips_account).
