---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Spark labs - Development environment
{: #lab_nsp}

Spark lab is a Spark-based development environment that enables you to interactively program, debug, submit, and test Spark applications on a Spark cluster running on the Spark engine.

It is available as a Visual Studio Code extension and you can install it in your local system to access Spark IDE using Visual Studio Code. It reduces the time for development and increases usability.


## Before you begin
{: #lab_nsp-preq}


1. Install a desktop version of Visual Studio Code.
1. Install watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data).
1. Ensure you have public-private SSH key pair to establish SSH connection with the Spark lab. For more information about generating the key, open watsonx.data extension in Visual Studio Code, go to Details tab, see the section, Set up SSH on your machine.
1. Install the Visual Studio Code extension, **Remote - SSH** from [Visual Studio Code marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh).


## Procedure
{: #lab_nsp-preq-1}


## Creating a Spark lab
{: #creat_lab}

1. Install watsonx.data extension.

    a. Open Visual Studio Code. Click **Extensions**.

    b. Browse for the watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data) and install the extension.

    c. You can also see the watsonx.data icon in the left navigation window. Click the icon. The **Settings** window opens.


2. Configure the watsonx.data extension.

    a. Click **Go to Settings**. Configure the following items:

    * `Environment Type`: Select IBM Public cloud as the environment type.

    * `host`: Hostname of the region where your watsonx.data SaaS instance is provisioned, `<region>`.lakehouse.cloud.ibm.com`.

    * `watsonx-data`: Instance ID : CRN of the watsonx.data SaaS instance.

    * `username`: The user name by which you want to connect to watsonx.data IBM cloud instance. The format is - `ibmlhapikey_userid`. Here ,userid is the IBM id of the user connecting to the watsonx.data instance.

    * `privateKeyPath`: Path to your private SSH key file.

    * `publicKeyPath`: Path to your public SSH key file.

    b. Click **Refresh**. The Visual Studio code window prompts for IBM Cloud IAM APIkey of the user that you specified in setting field watsonx-data.userName. To generate the API key, see [Managing user API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui).

    c. Provide the API key and press Enter. Refresh your window to view the Spark engine in the left pane of Visual Studio Code application.

3. Create a Spark lab.

    a. To create a new Spark lab, click the + icon. The Create Spark Lab window opens. Specify your **public SSH key** and the **public SSH keys** of the users whom you want to grant access to Spark lab. Specify each public SSH key on a new line.

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
