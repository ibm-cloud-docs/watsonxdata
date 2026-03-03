---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-03"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata


---

{{site.data.keyword.attribute-definition-list}}

# Masking your data in watsonx.data on IBM Cloud with Azure Active Directory
{: #ikc_integration_ad_saas}


This topic describes how to integrate Azure Active Directory (Azure AD) as a SAML identity provider with watsonx.data on IBM Cloud .
You can configure Azure Active Directory (now Microsoft Entra ID) as your SAML identity provider to enable single sign-on (SSO) for watsonx.data IBM Cloud.

## Before you begin
{: #prereq_ikc-saas}

To enable IKC integration, ensure the following pre-requisites are met:

- A working {{site.data.keyword.lakehouse_short}} instance on IBM Cloud.
- Access to IBM Software Hub
- IBM Knowledge Catalog (IKC) on IBM Software Hub.
- Subscription to Microsoft Azure.


## Configuring Azure Active Directory application on IBM Cloud
{: #connect_prcd_saas}
{: step}

### Retrieving the SAML metadata file from your watsonx.data on IBM Cloud
{: #connect_import_ad-saas}


1. Log in to your IBM Cloud account.

1. Go to **Manage > Access (IAM) > Identity providers** in the IBM Cloud console.


3. Click **Add** and select **IBM Cloud SAML** as the provider type.

4. Enter a name for the provider (for example, `Azure AD`).

5. In the **Service Provider** section, all fields are pre-populated. Click **View advanced settings** and clear the **Authentication context** selection.

5. Click **Save**.

6. Click **Download configuration** to download the metadata service provider configuration.


### Configuring Azure Active Directory application
{: #connect_import_ad_cpd}

1. Log in to your Azure portal. Select the **Manage Microsoft Entra ID** tile and click **View**.

2. From the left menu, select **Enterprise applications**.

3. Click **New application**.

4. In the search bar, search for `IBMid`.

5. Select **IBMid** from the results and click **Create**. The **Overview** page opens.

9. Add users and groups to your application:
   1. On the **Overview** page, select the **1. Assign users and groups** tile from the **Getting started** section.

   2. Click **Add user/group**.

   3. On the **Add assignment** page, under **Users and groups**, click **None selected**. The list of users and groups opens in a **Users and groups** window.

   4. Select the users and groups that you want to add to your application from the list, and click **Select**.

   5. On the **Add assignment** page, click **Assign**.

   6. Go back to your application overview.

6. In the **Getting Started** section, select **2. Set up single sign-on**.

6. Click **SAML**. The **Basic SAML Configuration** page opens.

7. At the top of the page, choose **Upload metadata file**.

8. Browse to and upload the metadata service provider configuration file downloaded in [Retrieving the SAML metadata file from your watsonx.data on IBM Cloud](#connect_import_ad-saas). This automatically populates the required configuration fields.

10. On the **Single Sign-On with SAML** page, click **Edit** to modify the **Attributes and Claims**.

11. Edit the **Unique User Identifier** value to `user.email` and save the details.

12. Leave the remaining options unchanged. Under **SAML Certificates**, copy the URL from the **Federation Metadata XML** attribute.

13. Open the copied URL in a new browser tab, copy the content, and save it as an XML file.

14. Ensure that the user accounts in Entra ID have all required attributes populated (email, first name, last name, and display name).

## Configuring Azure Active Directory application on IBM Software Hub
{: #connect_import_ad_cpd}
{: step}


1. Complete the [configuration steps](https://www.ibm.com/docs/en/cloud-paks/foundational-services/4.x_cd?topic=configuration-integrating-saml-entra-id#ariaid-title5) in the [Microsoft Azure portal](https://portal.azure.com/auth/login/) and save the Federation Metadata XML to your local drive.

When you upload the Federation Metadata XML configuration to watsonx.data on IBM Software Hub, update the token attribute-mapping fields such as Email, Family name, Given name, Groups and Sub with the following values: \n
   * Email : http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress
   * Family name : http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
   * Given name : http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
   * Groups : http://schemas.microsoft.com/ws/2008/06/identity/claims/groups
   * Sub : http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress
{: important}

## Upload the Federation Metadata XML configuration to watsonx.data on IBM Cloud
{: #upload_import_ad_-saas}
{: step}

Complete these steps from watsonx.data on IBM Cloud.


1. Log in to your IBM Cloud account.

1. Go to **Manage > Access (IAM) > Identity providers** in the IBM Cloud console.

2. You should now be on the **Identity Provider Details** page.

3. Upload the XML file created in [Configuring Azure Active Directory application](#connect_import_ad_cpd). This automatically populates the required fields.

3. After uploading the XML file, if you encounter an issue with the IAM claim name in the assertion mapping section, map the SAML assertion `http://schemas.microsoft.com/identity/claims/displayname` to the IAM claim name.

4. Click **Verify** to test the SAML connection between IBM Cloud (Service Provider) and Azure AD (Identity Provider).

5. Authenticate when prompted and confirm that a **Connection succeeded** message is displayed.

6. Once verification is successful, save the configuration. Leave the attribute mapping unchanged unless additional fields are required.

7. After saving, navigate back to **Identity providers** from the left menu.

8. Confirm that the Azure AD provider is listed, and toggle the **Enable** option to activate it.

9. Copy the **Login URL** from the provider tile and share it with Azure AD users. Each user must authenticate at least once using this URL to be added to the IBM Cloud account.



## Verify the configuration by testing the intergration
{: #upload_import_ad_-saas}
{: step}


## Configure IKC in {{site.data.keyword.lakehouse_full}} UI
{: #conf_ikc}
{: step}

1. Log in to {{site.data.keyword.lakehouse_full}}.
1. From the left pane, go to **Access control**.
1. Select the catalog to open the catalog details page.
1. Go to the **Integrations** tab and click **Integrate service**.
1. Enter the following details:

   | Field | Description |
   |-------|-------------|
   | Service | Select **IBM Knowledge Catalog**. |
   | Cluster type | Select **Software** |
   | Supported catalogs | Select the applicable catalogs for IKC governance. |
   | IKC endpoint  | Specify the Knowledge Catalog endpoint URL. For example, https://<instance>.ibm.com. |
   | Username | Enter your username (`ibmlhapikey_<EMAIL_ID>`). |
   | Password | Specify the Zen API key. For more information, see [Generating token](https://www.ibm.com/docs/en/software-hub/5.3.x?topic=keys-generating-zenapikey-authorization-tokens). |
   |Port is SSL enabled | Use the toggle switch to enable or disable SSL connection. Enabling the SSL connection ensures secure connection.  |
   |Upload Certificate | If SSL is enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert, or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert, or .cer) link. \n iii. Browse the SSL certificate and upload. \n From the cluster where IKC is installed, you can retrieve the certificate using the following steps: \n a. Click on Not Secure in the address bar. \n b. Select Certificate details from the drop-down. \n c. Switch from the General tab to the Details tab. \n d. Click on Export to save the certificate. |
   | Test connection | Click the Test connection link to verify the connection. If the connection is successful, you can view a success message. |
   {: caption="Ingrate service" caption-side="bottom"}

1. Click **Integrate**.

### Generating a Keystore and a Key pair
{: #ikc}


1. Log into your IKC server by using SSH and use the following command to generate a new keystore file containing a private key and a self-signed certificate.

``` bash
keytool -genkey -keyalg RSA -alias ikcadmin -keystore ikc-admin-keystore.jks -storepass <store_password> -validity 365 -keysize 2048 -dname "CN=<Ikc FQDN>, OU=<Organizational Unit>, O=<Organization>, L=<City>, ST=<State>, C=<Country>"
```
{: codeblock}


Replace `<store_password>` with a strong password.
Replace `<Ikc FQDN>` with the server's FQDN (e.g., ikc.example.com).
Provide appropriate values for Organizational Unit (OU), Organization (O), Location (L), State (ST), and Country (C) when prompted, or by using the -dname parameter.




## Verify the masking functionality as per the rules in IKC
{: #verify_mask-saas}
{: step}

1. Log in to IBM Knowledge Catalog.
1. From the left pane, go to **Governance** > **Rules**.
1. From the **Rules** page, verify that the rules corresponding to your data class of the column is defined. You can define a new rule by using **Add rule** button.

The owner can see the unmasked data. To verify whether masking is functioning correctly, log in to {{site.data.keyword.lakehouse_short}} as user who is not the owner of the asset in IKC and query the asset.
{: note}
