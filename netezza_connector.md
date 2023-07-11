---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

keywords: lakehouse, netezza, connector, watsonx.data

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

# Netezza connector for Presto
{: #netezza_connector}

Netezza connector for Presto is a customized connector for {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

For more information about SQL statements supported by Netezza connector, see [Supported SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements){: external}.

## Connectivity
{: #nz_connectivity}

To connect Presto to your Netezza database, you need the following database details and connect credentials.

### Database details
{: #database_details}

To connect Presto to your Netezza database, you need the following database details.

| Database detail | Description |
|-----------------|----------------|
| Host name | The hostname of the server.|
| Port number | Used by the database manager for TCP/IP communication.|
| Database name | The name of the Netezza database|
{: caption="Table 1. Database details" caption-side="bottom"}

### Connection credentials
{: #connect_credentials}

To connect Presto to your Netezza database, you need the following connection credentials.

| Credential | Description |
|-------------|----------------|
| Netezza database credentials | Use your database user ID and password.|
{: caption="Table 12. Connection credentials" caption-side="bottom"}

## Configuring Netezza connector
{: #config_netezza}

1. Create a `netezza.properties` file inside the **etc/catalog** folder of Presto.

2. Add the following properties to the `netezza.properties` file.

   `connector.name=netezza`

   `connection-url=jdbc:netezza://<hostname>:<port>/<database name>`

   `connection-user=<user name>`

   `connection-password=<password>`

   `allow-drop-table=<true/false>`

If you want to create multiple catalogs for Netezza, name the properties files with respective catalog names.

## Limitations
{: #limitations_netazza_con}

Netezza connector partially supports `CREATE VIEW` statement. The Presto Supported SQL syntax does not include creating views with custom column names (different than the table column names).
