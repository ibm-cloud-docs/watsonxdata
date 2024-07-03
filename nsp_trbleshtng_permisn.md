---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Why do I receive permission denied error while connecting to Spark labs?
{: #ts-nsp-permsn}
{: troubleshoot}

When you try to establish a connection with Spark labs, a "Permission denied" error is displayed.
{: tsSymptoms}

Your SSH connection is not using the right private key to authenticate with the Spark labs.
{: tsCauses}

Ensure the following to resolve the issue.
{: tsResolve}

1. The extension settings use the correct SSH private and public key pairs (**PrivateKeyPath** and **PublicKeyPath**).
2. Use the same public key in the **Settings** page and in the **Create Spark Lab** window.
4. Add an entry to your SSH configuration under ~/.ssh/config. Specify `<port_number>` and `~/.ssh/id_rsa` in the following configuration.

    ```bash
    Host cpdenv
        HostName localhost
        Port <port_number> # Same port as spark-labs.localPort
        IdentityFile ~/.ssh/id_rsa # Path to your private key

    ```
    {: codeblock}
