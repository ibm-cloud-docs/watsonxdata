---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring and debugging Spark applications from Spark labs
{: #lab_mon_nsp}



## Debugging the Spark application from Spark labs
{: #lab_nsp-deug}

The Spark lab helps to debug the Spark application that you submit. To do that:


1. Go to Visual Studio Code > **Extensions**.
1. Browse for the debugging tool to debug the code. For each Spark application type (Python, Java, Scalar, R), you need to choose the official extension to debug. For example, if you submit a Spark application that is written in the Python language, install the **Python** extension.
1. Open the file that you want to debug and click **Run and Debug** from the Visual Studio Code after you install the debugging tool extension. The Visual Studio Code window prompts for the language of the Spark application code and default configuration.
1. Select the language and provide the default configuration based on your Spark application type (Python, Java, Scalar, R).
1. Click **Run and Debug**. The debugging process starts and you can view the results in the **Terminal**.


## Accessing Spark UI from Spark labs
{: #lab_nsp-ui}

The Spark user interface (UI) allows you to monitor various aspects of running a Spark application. For more information, see [Spark user interface](watsonxdata?topic=watsonxdata-wxd_spk_ui){: external}. Expose Spark UI to access it from Spark labs. To do that:

1. Go to Visual Studio Code > **Terminal** and select the **Ports** tab.
2. Click **Forward a Port**. Type `4040` and press **Enter**. You can now access Spark UI from Spark labs. Open a web browser and enter the URL in the format - `localhost:4040`. The Spark UI opens, which allows you to inspect Spark applications in the Spark labs. You can view the following details :

    * The **Event timeline** displays a graphical view of the timeline and the events.
    * Different stages of execution, the storage used, the Spark environment, and executor (memory and driver) details.
