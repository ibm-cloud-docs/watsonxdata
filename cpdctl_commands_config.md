---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-24"

keywords: lakehouse, cpdctl, watsonx.data, supporting commands, config

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

# config commands and usage
{: #cpdctl_commands_config}

The config command further has different commands within, using which you can configure {{site.data.keyword.lakehouse_full}} environment in IBM cpdctl. This topic lists the commands with brief description of the tasks that can be performed.

The config command manages the configuration of profile and users for {{site.data.keyword.lakehouse_short}}. The {{site.data.keyword.lakehouse_short}} instance must be open in the web browser while configuring and performing the operations.

   Syntax:

   ```bash
   ./cpdctl config [commands]
   ```
   {: codeblock}

The config command supports the following commands:
   * [user](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configuser)
   * [profile](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configprof)

   You can set [user](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configuser) and [profile](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configprof) by running these commands separately. It is recommended to use the combined commands to set the profile and users through a single command. For more information, see [Using the commands user and profile together](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configboth).
   {: tip}

## Configuring encryption key for IBM cpdctl
{: #cpdctl_commands_configencrypt}

To secure your passwords and API keys, IBM cpdctl uses AES-256 encryption. You can use a custom encryption key or the default hardcoded key provided by IBM cpdctl.

You can provide a custom encryption key for AES-256 by setting the CPDCTL_ENCRYPTION_KEY_PATH environment variable pointing to the path of encryption key file holding directory. If this environment variable is not set, cpdctl will use its own hardcoded encryption key.

For macOS and Linux:
   ```bash
   export CPDCTL_ENCRYPTION_KEY_PATH=/path/cpdctl.key
   ```
   {: codeblock}

For Windows Command Prompt:
   ```bash
   set CPDCTL_ENCRYPTION_KEY_PATH=/path/cpdctl.key
   ```
   {: codeblock}

For Windows PowerShell:
   ```bash
   $env:CPDCTL_ENCRYPTION_KEY_PATH = "/path/cpdctl.key"
   ```
   {: codeblock}

## user
{: #cpdctl_commands_configuser}

The `user` command manage users in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl config user [commands]
   ```
   {: codeblock}

The `user` command further supports the following commands:

| Options | Description |
| ---- | --- |
|`./cpdctl config user set [commands]`|Set the credentials for a user in cpdctl configuration to connect to {{site.data.keyword.lakehouse_short}} instance.|
|`./cpdctl config user list`|List the credentials stored in cpdctl configuration that is used to connect to {{site.data.keyword.lakehouse_short}} instance.|
|`./cpdctl config user get <username>`|Get the credentials of a user stored in cpdctl configuration that is used to connect to {{site.data.keyword.lakehouse_short}} instance.|
|`./cpdctl config user unset <username>`|Remove the currently set username from the cpdctl configuration of {{site.data.keyword.lakehouse_short}} instance.|
 {: caption="Supported commands by user" caption-side="bottom"}

`./cpdctl config user set [commands]` further supports the following commands as options to be used for setting the credentials:
   ```bash
   --apikey (string) : Set user apikey

   --password (string) : Set user password

   --token-file (string) : Set location of a file that contains user token

   --username (string) : Set user name
   ```
   {: codeblock}

Example setting up a user in a cloud instance:

   ```bash
   ./cpdctl config user set <user> --username <saas_username> --apikey <APIKEY>
   ```
   {: codeblock}

   ```bash
   ./cpdctl config user set user2 --username user@ibm.com --apikey APIKEY
   ```
   {: codeblock}

For {{site.data.keyword.lakehouse_short}} on IBM Cloud, it is recommended to use `--username` and `--apikey` which are used to login to the console. For more information see, [Get API key](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).


## profile
{: #cpdctl_commands_configprof}

The `profile` command manage profiles in {{site.data.keyword.lakehouse_short}}.

   Single sign-on (SSO) login is enabled in cpdctl configuration.
   {: note}

Syntax:
   ```bash
   ./cpdctl config profile [commands]
   ```
   {: codeblock}

The `profile` command supports the following commands:

|Options|Description|
| ---- | ---- |
|`./cpdctl config profile set [commands]`|Set {{site.data.keyword.lakehouse_short}} environment profile in cpdctl configuration.|
|`./cpdctl config profile list`|List all {{site.data.keyword.lakehouse_short}} environment profiles set in cpdctl configuration.|
|`./cpdctl config profile get <profilename>`|Get details of the {{site.data.keyword.lakehouse_short}} environment profile from cpdctl configuration.|
|`./cpdctl config profile unset <profilename>`|Remove {{site.data.keyword.lakehouse_short}} environment profile from cpdctl configuration.|
|`./cpdctl config profile current`|Get details of the current {{site.data.keyword.lakehouse_short}} environment profile used from cpdctl configuration.|
|`./cpdctl config profile use <profilename>`|Use a particular {{site.data.keyword.lakehouse_short}} environment profile from cpdctl configuration.|
{: caption="Supported commands by profile" caption-side="bottom"}

`./cpdctl config profile set [commands]` further supports the following commands as options to be used for setting the credentials:
   ```bash
   --apikey (string) : Create a user having this API key and associate it with the profile. Used for SaaS and Onprem. Recommended to use for SaaS instance.

   --common-services-url (string) : Set Common Services URL for the profile

   --iam-integration-enabled () : Set if IAM integration is enabled on CP4D

   --ibmcloud (string) : Connect the profile to IBM Cloud CLI session metadata. Flag value specifies IBM Cloud CLI configuration directory. If no value is given, default IBM Cloud CLI configuration directory is assumed.

   --password (string) : Create a user having this password and associate it with the profile. Used for Onprem. Recommended to use for Onprem instance.

   --region (string) : IBM cloud region.

   --token-file (string) : Create a user having this token location and associate it with the profile.

   --url (string) : Set URL for the profile

   --user (string) : Set user for the profile

   --username (string) : Create a user having this name and associate it with the profile.
   ```
   {: codeblock}

Example setting up a profile using teh `user` configuration set earlier in a cloud instance:

   ```bash
   ./cpdctl config profile set <profile_name> --user <user> --url <profile_url> --region <region_name>
   ```
   {: codeblock}

   ```bash
   ./cpdctl config profile set saas --user user2 --url https://cloud.ibm.com/ --region us-south
   ```
   {: codeblock}

## Using the commands user and profile together
{: #cpdctl_commands_configboth}

You can combine the 2 commands user and profile together to configure instance profile in cpdctl configuration. A sample illustration of how to use the combination is provided below:

**Setting up a cloud instance profile:**

Syntax:
   ```bash
   --env "WATSONX_DATA_INSTANCE_ID=<crn>" \
   --env "WATSONX_DATA_URL=<WXD-base-url>"
   ```
   {: codeblock}

Example:
   ```bash
   ./cpdctl config profile set saas --username user@ibm.com --apikey APIKEY --url https://cloud.ibm.com/ --region us-south \
   --env "WATSONX_DATA_INSTANCE_ID=crn:v1:staging:public:lakehouse:us-south:a/781f752068d44638a3b2a13de58d3cfe:2c590eda-8d51-4269-86ce-a6dfb84c8267::" \
   --env "WATSONX_DATA_URL=https://us-south.lakehouse.dev.cloud.ibm.com/"
   ```
   {: codeblock}

For {{site.data.keyword.lakehouse_short}} on IBM Cloud, it is recommended to use `--username` and `--apikey` which are used to login to the console. For more information see, [Get API key](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).

## Setting the instance ID as environment variable
{: #cpdctl_commands_configinstid}

Starting from cpdctl version 1.8.5, users no longer need to set the `instance ID` as environment variable. This method is deprecated and will be completely removed in a future release. Instead, you must set the `instance ID` directly using the <codeph>profile</codeph> command, as described in [Using the commands user and profile together](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config#cpdctl_commands_configinstid)
{: important}

You must set an instance ID to access the corresponding environment to run the cpdctl commands. To set the instance ID, you can use the `WX_DATA_INSTANCE_ID` environment variable. This allows you to avoid specifying the instance ID with each command.

To set the variable, run the following command in macOS and Linux:
   ```bash
   export WX_DATA_INSTANCE_ID=<instance-id_value>
   ```
   {: codeblock}

Where, `<instance-id_value>` is the instance ID of the {{site.data.keyword.lakehouse_short}} software instance or CRN of your {{site.data.keyword.lakehouse_short}} instance on IBM Cloud which can be accessed by clicking the i icon on the homepage.

To set the variable, run the following command in Windows Command Prompt:
   ```bash
   set WX_DATA_INSTANCE_ID=<instance-id_value>
   ```
   {: codeblock}

To set the variable, run the following command in Windows PowerShell:
   ```bash
   $env:WX_DATA_INSTANCE_ID = "<instance-id_value>"
   ```
   {: codeblock}
