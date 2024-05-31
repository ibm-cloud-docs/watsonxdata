---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: lakehouse, milvus, watsonx.data

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

# Connecting to Milvus service
{: #conn-to-milvus}

Run any one of the following commands to connect with Milvus:
{: shortdesc}

## By using API key:
{: #conn-to-milvusapikey}

```bash
print(fmt.format("start connecting to Milvus"))
connections.connect(host="<host>", port="<port>", secure=True, server_name="localhost", user="ibmlhapikey", password="<api-key>")
has = utility.has_collection("hello_milvus")
print(f"Does collection hello_milvus exist in Milvus: {has}")
```

## By using Token:
{: #conn-to-milvusatoken}

```bash
connections.connect(host="<host>", port="<port>", secure=True, server_name="localhost", user="ibmlhtoken", password="<token>")
```

## By using URI
{: #conn-to-milvusuri}

This an alternate method of connecting to Milvus instead of the `host` and `port` parameters.
{: note}

```bash
print(fmt.format("start connecting to Milvus"))
connections.connect( alias="default", uri="https://<host>:<grpc-port>", user = "ibmlhtoken", password = "token" )
has = utility.has_collection("hello_milvus")
print(f"Does collection hello_milvus exist in Milvus: {has}")
```
For getting API keys, see [Getting the IBM API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-api-iam-token){: external}.
