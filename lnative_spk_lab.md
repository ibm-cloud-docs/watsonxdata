---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-15"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with VS Code development environment
{: #lab_nsp}

The VS Code development environment is a Spark-based development environment that enables you to interactively program, debug, submit, and test Spark applications on a Spark cluster running on the Spark engine.

It is available as a Visual Studio Code extension and you can install it in your local system to access Spark IDE using Visual Studio Code. It reduces the time for development and increases usability.


## Before you begin
{: #lab_nsp-preq}


1. Install a desktop version of Visual Studio Code.
1. Install watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data).
1. Install the Visual Studio Code extension, **Remote - SSH** from [Visual Studio Code marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh).


As Spark labs are ephemeral in nature, you must back up the data stored periodically to prevent potential data loss during upgrades or a Spark master crash.
{: important}

## Procedure
{: #lab_nsp-preq-1}


## Setting up the Spark labs
{: #creat_lab}

1. Install watsonx.data extension.

    a. Open Visual Studio Code. Click **Extensions**.

    b. Browse for the watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data) and install the extension.

    c. You can also see the watsonx.data icon in the left navigation window. Click the icon. The **Welcome to IBM watsonx.data extension** window opens.


2. From the **Welcome to IBM watsonx.data extension** window, click **Manage Connection**. The **Manage Connection watsonx.data** window opens.

3. Configure one of the following details:

    * **JSON Inputs**

    * **Form Inputs**

4. To configure **JSON Inputs**, click **JSON Inputs** and specify the following details:

    * **API Key** : Provide the platform API key. To generate the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).
    * **Connection JSON** : Provide the connection details from the watsonx.data user interface. To do that:
        1. Log in to your watsonx.data page.
        2. Click **Infrastructure manager**.
        3. Click your Spark engine that is in running status. In the **Details** tab, from the **VS Code connection configuration** field, click the **View configurations** link. Copy the configuration and use this as the **Connection JSON** field value.

5. To configure **Form Inputs**, click **Form Inputs** and specify the following details:
    * **Host address of watsonx.data console** : Provide the host IP address of the watsonx.data install. To retrieve the host IP address, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    * **Environment Type** : Select `SAAS`.
    * **CRN** : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    * **Username** : Your email-id if you are using your API key or it should be in the format `<Service-id>-<GUID>`. For more information on generating service id and GUID, see [Creating service IDs](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws?topic=2u-granting-access-through-service-ids-api-keys-from-saas-console#creating_service_IDs).
    * **API Key** : Provide the platform API key. To generate the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).


3. Create a Spark lab.

    a. To create a new Spark lab, click the + icon. The **Create Spark Lab** window opens. Specify a unique name for the Spark lab and select the **Spark Version**. The default Spark version is 3.4. You can modify the other optional fields if required.

    The `spark.hadoop.wxd.apikey` parameter is configured in the **Spark configurations** field by default while creating Spark lab.
    {: note}

    b. Click **Create**. Click **Refresh** to see the Spark lab in the left window. This is the dedicated Spark cluster for application development.

    c. Open the Spark lab to access the file system, terminal, and work with it.

    c. In the **Explorer** window, you can view the file system, where you can upload the files, and view logs.

    To delete an already running Spark lab, hover the mouse over the name of the Spark lab in the watsonx.data left navigation pane and click on Delete icon.
    {: note}

## Developing a Spark application
{: #dev_lab}

Develop a Spark application in the Spark lab. You can work with a Spark application in one of the following ways:

* [Create your own Python file](#dev_lab_01)
* [Create Jupyter Notebooks](#dev_lab_02)

### Create your own Python file
{: #dev_lab_01}

1. Create, upload or drag the Python application file to the **Explorer** window. The file opens in the right pane of Visual Studio Code application.

2. Run the following command in the terminal. This initiates a Python session and you can see the acknowledgment message in the terminal.

    ```bash
    python <filename>
    ```
    {: codeblock}

### Create Jupyter Notebooks
{: #dev_lab_02}


1. Browse for the `Jupyter` extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) and install the extension.

2. You can either create a new Jupyter Notebook file with the extension `.ipynb` or drag and drop the existing notebook to the **Explorer** window.

3. From the **Explorer** window, double-click to open the Jupyter Notebook.

4. From the Jupyter Notebook, click the **Change Kernel** link to select the **Python Environment**.

5. The Jupyter Notebook is now ready to use. You can write your code and execute it cell by cell.
