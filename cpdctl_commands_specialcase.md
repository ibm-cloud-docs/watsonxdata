---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-23"

keywords: lakehouse, database, tags, description, watsonx.data

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
{:attention: .attention}
{:remember: .remember}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Additional information about `cpdctl wx-data` command usage and examples
{: #cpdctl_commands_specialcase}

This topic provides a few usage scenario guidance for the `cpdctl wx-data` command-line interface (CLI), covering various commands and their practical examples. While `cpdctl` offers a way to manage IBM® watsonx.data resources, some examples require platform-specific adjustments for successful execution. This topic highlights key scenarios where users, particularly those on Windows, need to modify the provided examples to align with their operating system. Additionally, it clarifies how JSON formatted key-value pairs are utilized within these commands and outlines the required formatting for Windows users.

   All the examples in this topic are referenced based on the examples you get using the help command explained in the "How to use wx-data command --help (-h)" section.
   {: attention}

## Scenario 1: Line Continuation or New Line Entry
{: #cpdctl_commands_specialcase1}

**macOS and Linux:** The backslash (`\`) character used in the help examples of `cpdctl wx-data` commands is used to indicate line continuation in multi-line `cpdctl` commands. This allows for improved readability when specifying complex command options.

   ```bash
   ./cpdctl wx-data engine attach \
       --id presto785 \
       --catalog-names icebergCatalog \
       --name presto \
       --instance-id 1234567890
   ```
   {: screen}

**Windows:** Windows command prompt and PowerShell do not support the backslash (\) for line continuation in the same way. Users must provide the entire command on a single line.

   ```bash
   cpdctl wx-data engine attach --id presto785 --catalog-names icebergCatalog --name presto --instance-id 1234567890
   ```
   {: screen}

## Scenario 2: JSON key value pairs in command options
{: #cpdctl_commands_specialcase2}

You can input JSON formatted options for cpdctl wx-data commands in one of the 2 ways listed:

   The example provided in this scenario is extracted partly from the --help output of Create for illustration purpose only.
   {: remember}

   * Many cpdctl wx-data commands utilize JSON formatted key value pairs to specify complex set of commands in a single set. These JSON strings can be directly incorporated into the command line, as seen in the help examples.

      ```bash
      --associated-catalog '{
          "catalog_name": "hivecos",
          "catalog_tags": ["tag_1", "tag_2"],
          "catalog_type": "hive-hadoop2"
        }'
      ```
      {: screen}

   * The OPTIONS in the cpdctl CLI --help output gives the single-line alternatives for the JSON key value pairs.

      ```bash
      --associated-catalog-name "hivecos" --associated-catalog-tags ["tag_1", "tag_2"] --associated-catalog-type "hive-hadoop2"
      ```
      {: screen}

## Scenario 3: JSON key value pairs usage formats in different operating systems
{: #cpdctl_commands_specialcase3}

**macOS and Linux:** When using JSON formatted key value pairs in macOS and Linux, the --help example formats provided can be used as is available.

   ```bash
   --associated-catalog '{
       "catalog_name": "hivecos",
       "catalog_tags": ["tag_1", "tag_2"],
       "catalog_type": "hive-hadoop2"
     }'
   ```
   {: screen}

**Windows:** When using JSON formatted key value pairs in Windows, the formatting must be adjusted to accommodate the command prompt and PowerShell's handling of quotation marks.

   * Windows Command Prompt: You must replace the single quotes (') surrounding the JSON string with double quotes (") and escape all internal double quotes (") with a backslash (\").

      ```bash
      --associated-catalog "{\"catalog_name\": \"hivecos\", \"catalog_tags\": [\"tag_1\", \"tag_2\"], \"catalog_type\": \"hive-hadoop2\"}"
      ```
      {: screen}

   * Windows PowerShell: All internal double quotes (") must be escaped with a backslash (\").

      ```bash
      --associated-catalog '{\"catalog_name\": \"hivecos\", \"catalog_tags\": [\"tag_1\", \"tag_2\"], \"catalog_type\": \"hive-hadoop2\"}'
      ```
      {: screen}
