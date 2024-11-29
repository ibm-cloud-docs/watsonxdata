---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-29"

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
{:attention: .attention}

# Birdwatcher debugging tool
{: #bd_dbgtool}

Birdwatcher is a command-line debugging tool for Milvus. Using Birdwatcher, you can connect to `etcd` or Milvus or both and check the state of the Milvus system.
{: shortdesc}

`etcd` is a metadata engine that manages the storage and access of metadata. This topic explains how to connect and execute Birdwatcher with `etcd`.

## Procedure

Birdwatcher is available inside the management container in `etcd` pod. Complete the following steps to log into `etcd` management container and execute Birdwatcher.

1. Run the following command to Get the `etcd` pod details based on the formation-id.

   ```bash
   i f <formation_id>
   ```
   {: codeblock}

   Example:

   ```bash
   i f f70eac82-0577-4887-a091-52aa2bc08463
   ```
   {: codeblock}

1. Login to the management sidecar of one of the `etcd` pods from the list.

   ```bash
   kubectl exec –it <etcd-pod> –c mgmt – bash
   ```
   {: codeblock}

   Example:

   ```bash
   kubectl exec –it c-f70eac82-0577-4887-a091-52aa2bc08463-etcd-m-0 –c mgmt – bash
   ```
   {: codeblock}

1. Run the following command to change the path.

   ```bash
   cd /temp
   ```
   {: codeblock}

1. Run the following command to execute Birdwatcher CLI.

   ```bash
   ./birdwatcher
   ```
   {: codeblock}

1. Run the following command to connect to `etcd`.

   ```bash
   connect --etcd <pod-dns-name>:2379 --enableTLS true --etcdCert /root/cert/tls.crt --etcdKey /root/cert/tls.key --rootCAPem /root/cert/ca.crt
   ```
   {: codeblock}

   Example:

   ```bash
   connect --etcd c-f70eac82-0577-4887-a091-52aa2bc08463-etcd-m.f70eac209152aabc0863eac2a0f8.svc.cluster.local:2379 --enableTLS true --etcdCert /root/cert/tls.crt --etcdKey /root/cert/tls.key --rootCAPem /root/cert/ca.crt
   ```
   {: codeblock}
