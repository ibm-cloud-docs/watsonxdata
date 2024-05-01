---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Spark lab
{: #lab_nsp}

Spark lab is a Spark-based development environment that enables you to interactively program, debug, submit, and test Spark applications on a Spark cluster running on the Spark engine.

It is available as a Visual Studio Code extension and you can install it in your local system to access Spark IDE using Visual Studio Code. It reduces the time for development and increases usability.


## Before you begin
{: #lab_nsp-preq}


1. Install a desktop version of Visual Studio Code.
1. Install watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data).
1. Ensure you have public-private SSH key pair to establish SSH connection with the Spark lab. For more information about generating the key, open watsonx.data extension in Visual 1. Studio Code, go to Details tab, see the section, Set up SSH on your machine.
1. Install the Visual Studio Code extension, **Remote - SSH** from [Visual Studio Code marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh).


## Procedure
{: #lab_nsp-preq-1}



1. Install watsonx.data extension.

    a. Open Visual Studio Code. Click **Extensions**.

    b. Browse for the watsonx.data extension from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.watsonx-data) and install the extension.

    c. You can also see the watsonx.data icon in the left navigation window. Click the icon. The **Settings** window opens.


2. Configure the watsonx.data extension.

    a. Click **Go to Settings**. Configure the following items:

    * `Environment Type`: Select IBM Public cloud as the environment type.

    * `watsonx-data.host`: Hostname of the region where your watsonx.data SaaS instance is provisioned, `<region>.lakehouse.cloud.ibm.com`.

    * `watsonx-data`: Instance ID : CRN of the watsonx.data SaaS instance.

    * `watsonx-data.username`: The user name by which you want to connect to watsonx.data IBM cloud instance. The format is - `ibmlhapikey_userid`. Here ,userid is the IBM id of the user connecting to the watsonx.data instance.

    * `watsonx-data.privateKeyPath`: Path to your private SSH key file.

    * `watsonx-data.publicKeyPath`: Path to your public SSH key file.

    b. Click **Refresh**. The Visual Studio code window prompts for IBM Cloud IAM APIkey of the user that you specified in setting field watsonx-data.userName. To generate the API key, see [Managing user API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui).

    c. Provide the API key and press Enter. Refresh your window to view the Spark engine in the left pane of Visual Studio Code application.

3. Create a Spark lab.

    a. To create a new Spark lab, click the + icon. The Create Spark Lab window opens. Specify your **public SSH key** and the **public SSH keys** of the users whom you want to grant access to Spark lab. Specify each public SSH key on a new line.

    b. Click **Create**. Click **Refresh** to see the Spark lab in the left window. This is the dedicated Spark cluster for application development.

    c. Open the Spark lab to access the file system, terminal, and work with it.

    c. In the **Explorer** window, you can view the file system, where you can upload the files, and view logs.

    To delete an already running Spark lab, hover the mouse over the name of the Spark lab in the watsonx.data left navigation pane and click on Delete icon.
    {: note}

4. Develop a Spark application in the Spark lab.

    a. Creating Spark context in Spark Lab. To create a Spark Context, you must explicitly set spark.master and spark.driver.host to the IP address of the Pod. The following example demonstrates on how to create a Spark context in python.

    ```bash
    from pyspark.sql import SparkSession
    import socket

    def getSparkMaster():
        ## getting the hostname by socket.gethostname() method
        hostname = socket.gethostname()
        ## getting the IP address using socket.gethostbyname() method
        ip_address = socket.gethostbyname(hostname)
        return ip_address

    def init_spark(sparkMaster):
      spark = SparkSession.builder.appName("auto-scale-test") \
              .master("spark://{}:7077".format(sparkMaster)) \
              .config("spark.driver.host",sparkMaster).getOrCreate()
      sc = spark.sparkContext
      return spark,sc
    ```
    {: codeblock}

    b. Create, upload or drag the Python application file to the **Explorer** window. The file opens in the right pane of Visual Studio Code application.

    c. Run the following command in the terminal. This initiates a Python session and you can see the acknowledgment message in the terminal.

    ```bash
    python <filename>
    ```
    {: codeblock}

## Debug the Spark application
{: #lab_nsp-preq-2}

The Spark lab also allows you to debug the Spark application that you submit. To do that:
1. Go to Visual Studio Code > **Extensions**.
1. Browse for the debugging tool to debug the code. For each Spark application type (Python, Java, Scalar, R), you need to choose the official extension to debug. For example, if you submit a Spark application written in Python language, install **Python** extension.
1. After you install the debugging tool extension, open the file that you want to debug and click **Run and Debug** from the Visual Studio Code.
1. The Visual Studio code window prompts for the language of the Spark application code and default configuration.
1. Select the language and provide the default configuration based on your Spark application type (Python, Java, Scalar, R).
1. Click **Run and Debug**. The debugging process starts and you can view the result in the **Terminal**.
