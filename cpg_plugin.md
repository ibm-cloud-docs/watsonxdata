---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-27"
keywords: cpg
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Common Policy Gateway (CPG) connector
{: #plug_cpg}

The Common Policy Gateway (CPG) connector is an advanced, plugin‑based lightweight JAR that serves as a flexible bridge between watsonx.data and a wide variety of external policy engines (IBM Knowledge Catalog, Apache Ranger). This client is designed to provide a flexible foundation that you can build upon, making it easy to develop, test, and deploy custom integrations.

At its core is the CPG Plugin Runner, a lightweight executable JAR that dynamically loads your access-control plugin JARs from a specified path (either absolute or relative). It evaluates plugins based on the configuration mapping and user-provided inputs such as  username,resources and actions.
It is available as a downloadable JAR file that can be easily downloaded and used to develop custom plugins that interface with multiple policy engines. You can build your own JARs tailored to specific policy engines, quickly test the integration.

## Before you begin
{: #plug_bfb}

You must:

   * Have the plugin JAR(s) (in PF4J format)

   * A policy mapping file defining the mapping of the plugins that should run for the corresponding policy engines.

## Downloading CPG package
{: #plug_proc}

1. Contact IBM Support team and get the latest version of CPG light weight package.

2. After downloading, unzip the package. The folder structure will look like this:

   ``` bash

   <bundle>/
   ├─ cpg.jar                   # The executable runner
   ├─ plugins/                  # Place your plugin JARs here
   │  └─ <your-plugin>.jar
   └─ config/
      └─ policy-config.yaml     # Maps resource names to plugin IDs

   ```
   {: codeblock}

   You can rename or move folders as required.
   {: note}

The package includes:

   * cpg.jar: The executable connector JAR that loads and runs your plugins.

   * plugins/: Directory to place your custom plugin JARs.

   * policy-config.yaml: Configuration file mapping watsonx.data resources to the policy engine plugin IDs. The following is an example of the `policy-config.yaml`.

   ``` bash

   plugin-mapping:
     hive_data:
       - java-access-plugin
       - go-access-plugin
     employee_table:
       - python-access-plugin
     iceberg:
       - go-access-plugin
     dicatalog/dischema/ditable/dicolumn:
       - ranger-presto-plugin

   ```
   {: codeblock}

   Parameters that are required in the configuration file:

   * **Keys**: The name of the watsonx.data resource(Example `hive_data`).

   * **Values**: Plugin IDs, defined in each plugin’s `plugin.properties` file. Example: `plugin.id=java-access-plugin`. The ID must match exactly.


## Building a plugin (from template) and configuring YAML
{: #plug_jar}

To connect to the required policy engine of your choice, you must create a plugin (JAR file) which compiles against the API types already embedded in `cpg.jar`. The downloaded CPG package includes a plugin template project. You can use the template and create a new one for your purpose. Additional dependencies are not required.

1. Unzip the template file.

1. Update the file to include the latest CPG jar file.

1. Run the following command:


   ``` bash
   cd java-access-plugin
   mvn -DskipTests clean package
   ```
   {: codeblock}

   Your JAR will be generated at: `target/<your-plugin>.jar`.

2. Copy the JAR into the CPG connector's `plugins/` folder.

3. Update `policy-config.yaml` to reference your plugin ID.

   Optional :To return row/column transforms, set them using: result.setTransformColumns(...); result.setTransformRows(...);


## Running CPG connector
{: #plug_con}

1. Run the CPG connector JAR file from the Terminal using the command: 'java -jar cpg.jar'.

   This will use the following default path for plugins and the config file.

   * plugins/ : ./plugins
   * config/  : ./config/policy-config.yaml

   You can also customize the path by using the following command:

   `java -jar cpg.jar <absolute/path/to/plugins> <absolute/path/to/config/policy-config.yaml>`.

   The following displays the sample interactive session:

   ``` bash

   Enter Username
   Enter resource_name (e.g., hive_data) or 'quit': hive_data
   Enter resource_type (e.g., table): table
   Enter actions (comma-separated, e.g., select,insert): select

   [Runner] Params: resource=hive_data, type=table, actions=[select]
   [Runner] Plugins to run: [java-access-plugin]
   [Runner] Results (1):
     -> ResourceAccessResult{
            resourceName='hive_data',
            actionsResult=[{select=true}],
            transformColumns={...},
            transformRows=...
     }

   ```
   {: codeblock}

2. Type quit or exit to stop.




## Troubleshooting
{: #plug_trb}


### Error: “No AccessPlugin extensions found”

If you get the above error, verify the following:

   * The plugins and directory exists and is not empty.
   * The JAR includes plugin.properties at its root.
   * The plugin class is annotated with @Extension and implements AccessPlugin.
   * The plugin.id in plugin.properties matches the ID in policy-config.yaml.

### Error: Plugin Not Running for Resource

If you get the above error, verify the following:

   * The resource name in `policy-config.yaml` maps correctly to the plugin ID.
   * The plugin IDs match exactly (case-sensitive).

### Error: Custom Paths Not Picked Up

If you get the above error, ensure to use absolute paths or pass them through system properties.


## Known Limitations:
{: #plug_lim}

The CPG plug in based connector has the following limitations:

   * Currently supports PF4J-based plugins only.

   * There is no user interface. Run using command-line interface.

   * Path resolution may vary between the OS environments.
