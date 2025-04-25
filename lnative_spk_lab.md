---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-22"

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

1. Subscription of {{site.data.keyword.lakehouse_short}} on Cloud. Ensure that you create a Spark engine and is in running status.
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

    * **API Key** : Provide the platform API key. To generate the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).
    * **Connection JSON** : Provide the connection details from the watsonx.data user interface. To do that:
        1. Log in to your watsonx.data page.

        2. From the navigation menu, click **Connection Information**.

        3. Click **VS Code**. Copy the configuration  from the **VS Code connection configuration** field and use this as the **Connection JSON** field value. For more information, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).


5. To configure **Form Inputs**, click **Form Inputs** and specify the following details:
    * **Host address of watsonx.data console** : Provide the **Host IP address** of the watsonx.data install. To retrieve the **Host IP address**, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    * **Environment Type** : Select `SaaS`.
    * **CRN** : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    * **Username** : Your email-id if you are using your API key or it should be in the format `<Service-id>-<GUID>`. For more information on generating service id and GUID, see [Creating service IDs](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws?topic=usca-granting-access-through-service-ids-api-keys-from-saas-console#creating_service_IDs).
    * **API Key** : Provide the platform API key. To generate the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).

4. Click **Test & Save**. `Retrieved Spark Clusters` message is displayed. The available Spark engines are displayed in the **WATSONX.DATA:ENGINES** section.

3. Create a Spark lab.

    a. To create a new Spark lab, from the **WATSONX.DATA:ENGINES** section, select the required Spark cluster and click the **+** icon (Add cluster) against it. The **Create Spark Lab** window opens. Specify a unique name for the Spark lab and select the **Spark Version**. The default Spark version is 3.5. You can modify the other optional fields if required.

    The `spark.hadoop.wxd.apikey` parameter is configured in the **Spark configurations** field by default while creating Spark lab.
    {: note}

    b. Click **Refresh** to see the Spark lab in the left window. This is the dedicated Spark cluster for application development.

    c. Click to open the Spark lab window to access the file system, terminal, and work with it.

    c. In the **Explorer** menu, you can view the file system, where you can upload the files, and view logs.

    To delete an already running Spark lab, hover the mouse over the name of the Spark lab in the watsonx.data left navigation pane and click on **Delete** icon.
    {: note}

## Developing a Spark application
{: #dev_lab}

Develop a Spark application in the Spark lab. You can work with a Spark application in one of the following ways:

* [Create your own Python file](#dev_lab_01)
* [Create Jupyter Notebooks](#dev_lab_02)

### Create your own Python file
{: #dev_lab_01}

1. From Visual Studio Code, click the Spark lab. A new window opens.

1. In the new Spark lab window, click **New File**. You get a **New File** prompt with the following file types:
   * **Text File** : Select to create a text file.
   * **Python File** : Select to create a Python application.
   * **Jupyter Notebook** : Select to create a Jupyter Notebook file.

1. Select **Python File**. A new `.py` file opens. You can start working on the Python file and save it later.

   You can also drag the Python application file to the **Explorer** page. The file opens in the right pane of Visual Studio Code application.
   {: note}

2. Run the following command in the terminal to execute your Python application. This initiates a Python session and you can see the acknowledgment message in the terminal.

    ```bash
    python <filename>
    ```
    {: codeblock}

### Create Jupyter Notebooks
{: #dev_lab_02}

1. From Visual Studio Code, click the Spark lab. A new window opens.

1. Install the `Jupyter` extension in the new Spark lab window to work with Jupyter Notebooks.
   From the **Extensions** menu in the new Spark lab window, browse for the `Jupyter` (You can also find it from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)) and install the extension.

   Make sure that you install the `Jupyter` extension from the new Spark lab window.
   {: note}

1. In the **Explorer** page, click **New File**. You get a **New File** prompt with the following file types:
   * **Text File** : Select to create a text file.
   * **Python File** : Select to create a Python application.
   * **Jupyter Notebook** : Select to create a Jupyter Notebook file.

   You can also create a new Jupyter Notebook file by typing the name of the file with the extension `.ipynb` or drag and drop the existing notebook to the **Explorer** page.
   {: note}

1. Select **Jupyter Notebook**. A new `.ipynb` file opens. You can start working on the Jupyter Notebook file and save it later.

1. From the Jupyter Notebook file, click the **Select Kernel** link.

1. You must select a **Python Environment** to run your file.

5. Select the file path that contains `conda/envs/python/bin/python`.

5. The Jupyter Notebook is now ready to use. You can write your code and execute it cell by cell.

When you save the file, the file path is automatically displayed in the **Save As** prompt. You can modify the path or Click **OK** to save.
{: note}
