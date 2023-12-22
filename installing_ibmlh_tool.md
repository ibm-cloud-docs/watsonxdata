---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

keywords: watsonxdata, tool, cli, command line interface

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

# Installing ibm-lh tool
{: #installing_ibmlh_tool}

An ingestion job in {{site.data.keyword.lakehouse_full}} is run with the **ibm-lh** tool. The tool must be pulled from the docker registry `docker://icr.io/ibm-lh-beta/` and installed to your local system to run the ingestion job through command-line interface (CLI).
{: shortdesc}

Do the following steps to install the **ibm-lh** tool:

1. From your local system, run the following command to login to Docker registry where the tool is located.

   If required, you can use Podman instead of Docker. If you use Podman, replace `docker` with `podman` in the commands.
   {: note}

   ```bash
   docker login -u iamapikey -p <IBM_cloud_api_key> icr.io
   ```
   {: codeblock}

2. Pull the tool image from the Docker registry.

   ```bash
   docker pull icr.io/ibm-lh-beta/ibmlh-datacopy:v1.0-beta
   ```
   {: codeblock}

3. Run the container image.

   ```bash
   docker run --name ibm-lh-tools -dt icr.io/ibm-lh-beta/ibmlh-datacopy:1.0-beta
   ```
   {: codeblock}

4. Run the following command to start the **ibm-lh** tool.

   ```bash
   docker exec -it ibm-lh-tools bash
   ```
   {: codeblock}
