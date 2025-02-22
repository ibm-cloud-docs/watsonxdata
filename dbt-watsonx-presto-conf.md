---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-22"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# dbt Configuration (setting up your dbt profile)
{: #dbt_watsonx_presto_conf}

To connect dbt Core to your Presto engine, configure the `profiles.yml` file that is located in `.dbt` of your home directory.

You can either copy or export the presto connection details to create the profiles.yml. To do that, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
{: note}

The following is an example configuration:

```bash
my_project:
  outputs:
    saas:
      type: presto
      method: BasicAuth
      user: username
      password: api_key
      host: <host>
      port: <port>
      database: analytics
      schema: dbt_drew
      threads: 8
      ssl_verify: true

  target: saas
```
{: codeblock}

The following table covers the parameter details:

| Option | Required/Optional | Description | Example |
| ------ | ----------------- | ----------- | ------- |
| `method` | Optional (default value is none) | Authentication method for Presto. | None or `BasicAuth` |
| `user` | Required | Username for authentication. | drew |
| `password` | Required if method is `BasicAuth` | Password or API key for authentication. | None or alphanumeric (abc123) |
| `http_headers` | Optional | HTTP headers to send alongside requests to Presto, specified as a yaml dictionary of (header, value) pairs. | X-Presto-Routing-Group: my-cluster |
| `http_scheme` | Optional (default is `http` or `https` for method: `BasicAuth`) | HTTP scheme to use (`http` or `https`). | `https` or `http` |
| `database` | Required | Catalog name for building models. | Analytics |
| `schema` | Required | Schema for building models. | dbt_drew |
| `host` | Required | Hostname for connecting to Presto. You can get the hostname by clicking View connect details in the engine details page. | 127.0.0.1 |
| `port` | Required | Port for connecting to Presto. You can get the port by clicking View connect details in the engine details page. | 8080 |
| `threads` | Optional (default is 1) | Number of threads for dbt operations. | 8 |
| `ssl_verify` | Optional | Path to the SSL certificate.  | `path/to/certificate` |
{: caption="Parameter details" caption-side="bottom"}

To obtain the SSL certificate, run the following command and save the certificate to the specified location.

```bash
openssl s_client -showcerts -connect <host>:<port>
```
{: codeblock}
