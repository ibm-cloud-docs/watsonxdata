---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

keywords: watsonxdata, qhmm

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

# Heap and thread memory dump
{: #heap_qhmm}

Heap and thread dumps allows you to view and identify memory-related usage issues of an engine. You can create heap and dump on a request basis with the help of an Administrator. After you generate the script, the memory-related diagnostic data will be available in Minio storage.
{: shortdesc}

The topic describes the following functions :

* [Creating heap and thread memory dump](#ret_pr_qhmm-heap)
* [Extracting heap and thread memory dump data](#extrct)



## Creating heap and thread memory dump
{: #ret_pr_qhmm-heap}

An administrator can create the heap and thread memory dumps either by using API or by starting an existing shell script that is packaged along with Presto.

* [Creation of heap and memory dump by using API](#api)

* [Creation of heap and memory dump by using Shell script](#shell)


### Creation of heap and memory dump by using API
{: #api}

The API can trigger the `heap_thread_dumper.sh` shell script for creating the heap and thread memory dump. This API allows you to initiate heap and thread memory dump creation on-demand by sending an HTTP POST request with the following details:

Endpoint URL: `https://localhost:8481/v1/lh_engine/dump`

GET Request:

``` bash
{
    "type": "thread",
    "file_name": "test",

}
```
{: codeblock}

The `type` can be set to either `thread` or `heap` depending on the type of dump you want to create.
The `file_name` is optional and is used to provide a custom name for the dump file.



Run the following CURL command to trigger heap or thread memory dump creation:

Example:

``` bash
curl --location 'https://localhost:8481/v1/lh_engine/dump' \
--header 'secret: <LH-instance-secret>' \
--header 'Content-Type: application/json' \
-k \
--data '{
    "type": "thread",
    "file_name": "test"
}'
```
{: codeblock}

### Creation of heap and memory dump by using Shell script
{: #shell}

The `heap_thread_dumper.sh` shell scripts present in {{site.data.keyword.lakehouse_short}} facilitates the creation of both heap and thread memory dumps.

1. Log in to the {{site.data.keyword.lakehouse_short}} instance where the Presto pods or Docker containers are running.

1. Navigate to the folder in the Presto pod or Docker container where the `heap_thread_dumper.sh` shell script resides.

1. Specify the parameter values and start the `heap_thread_dumper.sh` shell script by using the following command. This manually triggers the heap memory dump creation.


    ``` bash
    cd /scripts./heap_thread_dumper.sh -f `<filename_without_extension>` -t `<thread|heap>` -c `<maximum_dump_files>`
    ```
    {: codeblock}


    Parameter values:

    `<filename_without_extension>`: The filename of the dump files.
    `<thread|heap>`: Specifies whether to create a thread or a heap memory dump.
    `<maximum_dump_files>`: The maximum number of dump files to be retained before rolling and archiving.


    Example shell script:

    cd /scripts./heap_thread_dumper.sh -f presto_node_01 -t heap -c 5



## Extracting heap and thread memory dump data
{: #extrct}

Retrieve heap and thread memory dump data from the MinIO storage using teh following procedure.

1. Log in to **MinIO** user interface.

1. Go to **Object Browser**. Click `wxd-system` storage.

1. In this storage, click `qhmm` folder.

1. In the `qhmm` folder, navigate to the specific instance (unique identification of the instance - `LH_INSTANCE_ID`. Get the `LH_INSTANCE_ID` from the watsonx.data console UI) and go to the `Presto` folder.

1. Inside the `Presto` folder, locate and navigate to `engine-id` (specific `engine ID` within the engine type. Get the `engine ID` from the watsonx.data console UI).

1. From the `engine-id` folder, navigate to `QueryHistory` folder.

1. Diagnostic data within the `QueryHistory` folder is organized based on date. The folder name format is `dt=<dd-mm-yyyy>`.

1. Inside each date folder, the data is organized based on the user who executes the queries. The folder name format is `user=<name>`.

1. Use the checkbox(multi or single select) to select the data you want to download and click **Download** button.
