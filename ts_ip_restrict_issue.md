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

If you enable IP address restriction in {{site.data.keyword.cloud_notm}}, you cannot use {{site.data.keyword.lakehouse_short}} because logging in from a restricted IP address is not allowed.
{: shortdesc}

## Workaround
{: #workaround}

Add the IP address available in the regional Cloudflare trace page to the allowed IP address list.

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

For more information, see [Allowing specific IP addresses for an account](https://cloud.ibm.com/docs/account?topic=account-ips&interface=ui#ips_account).
