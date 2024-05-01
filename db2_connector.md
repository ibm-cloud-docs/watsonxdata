---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: lakehouse, Db2, connector, watsonx.data

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
{:note: .note}

# Db2 connector for Presto
{: #db2_connector}

Db2 connector for Presto is a customized connector for {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

For more information about SQL statements supported by Db2 connector, see [Supported SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements){: external}.

## Connectivity
{: #db2_connectivity}

To connect Presto to your Db2 database, you need the following database details and connect credentials.

### Database details
{: #db2_database_details}

To connect Presto to your Db2 database, you need the following database details.

| Database detail | Description |
|-----------------|----------------|
| Host name | The hostname of the server.|
| Port number | Used by the database manager for TCP/IP communication.|
| Database name | The name of the Db2 database.|
{: caption="Table 1. Database details" caption-side="bottom"}

### Connection credentials
{: #db2_connect_credentials}

To connect Presto to your Db2 database, you need the following connection credentials.

| Credential | Description |
|-------------|----------------|
| IBM ID| IBM ID is the ID that you used to log in to IBM Cloud. **NOTE:** Do not use the ID that you use to connect applications or tools to your Db2 database.|
| Db2 database credentials | Use your database user ID and password.|
| Administrator-created users | Db2 Warehouse and some Db2 managed service plans allow administrative users to create new users. These administrator-created user IDs and passwords can be used to log in to the web console URL and connect to the Db2 database from applications or tools.|
{: caption="Table 12. Connection credentials" caption-side="bottom"}


If you are not the owner or administrator of your Db2 instance, you can get your database details and connect credentials from your administrator.
{: note}


## Configuring Db2 connector
{: #config_db2}

1. Create a `db2.properties` file inside the **etc/catalog** folder of Presto.

2. Add the following properties to the `db2.properties` file.

   `connector.name=db2`

   `connection-url=jdbc:db2://<hostname>:<port>/<database name>`

   `connection-user=<user name>`

   `connection-password=<password>`

   `allow-drop-table=<true/false>`

If you want to create multiple catalogs for Db2, name the properties files with respective catalog names.

## Limitations
{: #limitations_db2_con}

1. In Db2, the schema can be dropped only if it is empty. Initiating `DROP SCHEMA` statement against a nonempty schema is expected to result in Db2 SQL Error `SQLCODE=-478` and `SQLSTATE=42893`.

2. Db2 connector partially supports `CREATE VIEW` statement. The Presto supported SQL syntax does not include creating views with custom column names (different than the table column names).
