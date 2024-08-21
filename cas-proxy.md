---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-21"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Using Data Access Service (DAS) proxy to access S3 and S3 compatible buckets
{: #cas_proxy}

External applications and query engines can access the S3 and S3 compatible buckets that are managed by {{site.data.keyword.lakehouse_short}} through DAS proxy.

To access the S3 and S3 compatible buckets:

1. Get the DAS endpoint from the {{site.data.keyword.lakehouse_short}} information window. Click the `i` icon on the home page to open the information window.
1. Replace the S3 endpoint with the DAS endpoint in your Java code.

   ```bash
   <DAS endpoint>/cas/v1/proxy
   ```
   {: codeblock}

1. Replace the access key with the encoded value in the Java code as follows:

      ```bash
      base64{<crn>|Basic base64{ibmlhapikey_<user_id>:<IAM_APIKEY>}}
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

## Java code example to use DAS
{: #jcode_xmp}

```bash
        String bucketName = "bucket1";
        String keyName = "folder1/file1";
        # replace the target object store endpoint with the DAS proxy endpoint
        String endpoint = "<DAS endpoint get from About page>/cas/v1/proxy";
        /** Replace the Access Key with watsonx.data user name and API key following the below base64 encoded method.
        * For Cloud Pak for Data: base64{<instanceid>|ZenAPIkey base64{username:<apikey>}}
        * For IBM Cloud: base64{<crn>|Basic base64{ibmlhapikey_<user_id>:<IAM_APIKEY>}}
        * For AWS: base64{<crn>|Basic base64{ibmlhapikey_ServiceId-<service_id>:<APIKEY>}}
        */
        String accessKey = "encoded value";
        String secretKey = "any string";

        BasicAWSCredentials cos_cred = new BasicAWSCredentials(accessKey, secretKey);
        EndpointConfiguration cosEndPoint = new EndpointConfiguration(endpoint, "us-east");
        AmazonS3 s3Client = AmazonS3ClientBuilder.standard().withPathStyleAccessEnabled(true)
                .withCredentials(new AWSStaticCredentialsProvider(cos_cred))
                .withEndpointConfiguration(cosEndPoint).build();
        GetObject.GetObjectTest(s3Client, bucketName, keyName);
```
{: codeblock}

For information about S3 REST API permissions, see [S3 REST API permissions]({{site.data.keyword.ref-role_priv-link}}#s3restapi){: external}.
{: note}
