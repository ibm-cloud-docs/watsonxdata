---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-04"

keywords: lakehouse, cpdctl, watsonx.data, download, install

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

# Downloading and installing IBM Cloud Pak for Data Command Line Interface (IBM cpdctl)
{: #cpdctl_install}

This topic provides information on how to download, install, and verify the IBM Cloud Pak for Data Command Line Interface (IBM cpdctl), with a focus on the {{site.data.keyword.lakehouse_full}} (`wx-data`) plugin.

## Before you begin
{: #cpdctl_installbyb}

You can learn more about IBM cpdctl from the official [README](https://github.com/IBM/cpdctl/tree/v1.6.95?tab=readme-ov-file#readme) file.

## Procedure
{: #cpdctl_installprcd}

1. Download and install IBM cpdctl using one of the following 2 methods:

   a. Option 1: Run the following command to automatically download and install the IBM cpdctl, detecting the operating system and processor architecture for Linux and macOS:

      ```bash
      platform=$(uname -s | tr '[A-Z]' '[a-z]')
      arch=$(uname -m | sed 's/x86_64/amd64/')
      curl -LOs "https://github.com/IBM/cpdctl/releases/latest/download/cpdctl_${platform}_${arch}.tar.gz"
      tar zxf cpdctl_${platform}_${arch}.tar.gz
      ```
      {: codeblock}

   b. Option 2: Download the appropriate archive from IBM cpdctl repository.

   IBM cpdctl for Windows operating system can be downloaded from the archive.
   {: note}

   | Operating system | Archive name | Comments |
   | --- | --- | --- |
   | Microsoft Windows x64 | `cpdctl_windows_amd64.zip` | Use the Windows Explorer to extract `cpdctl.exe` from the archive. |
   | Linux x64 | `cpdctl_linux_amd64.tar.gz` | Issue command `$ tar zxf cpdctl_linux_amd64.tar.gz` to extract the cpdctl executable from the archive. |
   | Linux Power 64 bit LE | `cpdctl_linux_ppc64le.tar.gz` | Issue command `$ tar zxf cpdctl_linux_ppc64le.tar.gz` to extract the cpdctl executable from the archive. |
   | Linux on IBM Z | `cpdctl_linux_s390x.tar.gz` | Issue command `$ tar zxf cpdctl_linux_s390x.tar.gz` to extract the cpdctl executable from the archive |
   | macOS - Intel x64 | `cpdctl_darwin_amd64.tar.gz` | Issue command `$ tar zxf cpdctl_darwin_amd64.tar.gz` to extract the cpdctl executable from the archive |
   | macOS - Apple silicon | `cpdctl_darwin_arm64.tar.gz` | Issue command `$ tar zxf cpdctl_darwin_arm64.tar.gz` to extract the cpdctl executable from the archive. |
   {: caption="Downloadable files for various operating systems" caption-side="bottom"}

   | {{site.data.keyword.lakehouse_short}} version | cpdctl version |
   | --- | --- |
   | v2.1.1 | v1.6.95 and later |
   | v2.1.1 (Developer edition) | 1.6.104 and later |
   | v2.1.2 | v1.7.0 and later |
   | v2.2.1 (V3 API) | v1.8.25 and later |
   {: caption="Supported cpdctl versions" caption-side="bottom"}

   MCSP is supported for CPDCTL from version v1.8.0 and later.
   {: note}


2. Run `./cpdctl` in the terminal to verify if cpdctl is installed successfully and to display the supported commands.

   Result is:
   ```bash
   NAME:
     cpdctl - IBM Cloud Pak for Data Command Line Interface

   USAGE:
      cpdctl [command] [options]

   COMMANDS:
     config         Manage Configuration
     asset          Manage Assets
     project        Manage Watson Studio - Projects API - OpenAPI Docs.
     space          Manage Spaces
     connection     Manage IBM Watson Data Platform Connections service.
     environment    Manage Environments and Runtimes API.
     notebook       Manage Notebooks API.
     code-package   Manage Code Packages API.
     job            Manage IBM Watson Data Platform Jobs and Scheduling Service.
     ml             Manage Watson Machine Learning.
     datastage      Manage IBM APIs for DataStage.
     find           Find a resource with CPD Path
     pipeline       Manage IBM Orchestration Pipelines API.
     wx-data        Manage watsonx.data.
     wx-ai          Manage watsonx.ai.
     version        Display the tool version

   OPTIONS:
         --cpd-config string   Configuration file path
         --cpdconfig string    [Deprecated] Use --cpd-config instead
     -h, --help                Show help
         --profile string      Name of the configuration profile to use
         --raw-output          If set to true, single values in JSON output mode are not surrounded by quotes
     -v, --version             Version of the plugin.

   Use "cpdctl service-command --help" for more information about a command.
   ```
   {: codeblock}
