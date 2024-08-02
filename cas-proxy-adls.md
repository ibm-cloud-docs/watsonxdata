---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-02"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Using Content Aware Storage (CAS) to access ADLS and ABS compatible buckets
{: #cas_proxy_adls}

External applications and query engines can access the Azure Data Lake Storage (ADLS) and Azure Blob Storage (ABS) compatible buckets that are managed by {{site.data.keyword.lakehouse_short}} through CAS proxy.

CAS proxy support for ADLS and ABS works only with AccountKey to pass {{site.data.keyword.lakehouse_short}} credential. Using SASToken to pass {{site.data.keyword.lakehouse_short}} credential is not supported.
{: important}

To access the ADLS and ABS compatible buckets:

1. Get the CAS endpoint from the {{site.data.keyword.lakehouse_short}} information window. Click the `i` icon on the home page to open the information window.
2. Replace the ADLS or ABS endpoint with the CAS endpoint in your Java code. Replace the access name with the encoded value as follows:

    **[IBM Cloud]{: tag-blue}**
      ```bash
      base64{<crn>|Basic base64{ibmlhapikey_<user_id>:<IAM_APIKEY>}}
      ```
      {: codeblock}

    **[Amazon Web Services (AWS)]{: tag-magenta}**
      ```bash
      base64{<crn>|Basic base64{ibmlhapikey_ServiceId-<service_id>:<APIKEY>}}
      ```
      {: codeblock}


      To get the Base64 encoded string, use one of the following commands:

      ```bash
      printf "username:<apikey>" | base64
      ```
      {: codeblock}


      ```bash
      echo -n "username:<apikey>" | base64
      ```
      {: codeblock}

3. Replace the container name in the Java code as follows:

   ```bash
   cas/v1/proxy/<bucketname in watsonx.data>
   ```
   {: codeblock}

## Java code example to use CAS
{: #jcode_xmp}

```bash
      //For IBM Cloud <ADLS or ABS account name>|base64{<crn>|Basic base64{ibmlhapikey_<user_id>:<IAM_APIKEY>}}
      //For AWS <ADLS or ABS account name>|base64{<crn>|Basic base64{ibmlhapikey_ServiceId-<service_id>:<APIKEY>}}
      String accountName = "<ADLS or ABS account name>|base64{<instanceid>|ZenApikey base64{username:<apikey>}}";
      String accountKey = "any string";
      String endPoint = "<CAS endpoint>";
      String containerName ="cas/v1/proxy/<bucketname in watsonx.data>";
      String endpoint = String.format(endPoint,accountName);

      BlobServiceClient blobServiceClient = new BlobServiceClientBuilder()
                .endpoint(endpoint)
                .credential(new StorageSharedKeyCredential(accountName, accountKey))
                .buildClient();

      BlobContainerClient containerClient = blobServiceClient.getBlobContainerClient(containerName);
```
{: codeblock}
