---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-19"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata


---

{{site.data.keyword.attribute-definition-list}}

# Configuring watsonx.data on IBM Software Hub with Azure Active Directory
{: #ikc_integration_ad}


This topic describes how to integrate Azure Active Directory (Azure AD) as a SAML identity provider with watsonx.data on IBM Software Hub.

## Before you begin
{: #prereq_ikc}

To enable IKC integration, ensure the following pre-requisites are met:

- A working {{site.data.keyword.lakehouse_short}} instance on IBM Cloud.
- A working {{site.data.keyword.lakehouse_short}} on IBM Software Hub.
- Subscription to Microsoft Azure.


## Retrieving the SAML metadata file from your watsonx.data on IBM Software Hub
{: #connect_import_ad}
{: step}

1. Log in to your watsonx.data on IBM Software Hub as an admin user.

1. Click **Identity providers > New connection**.

1. Select **SAML 2.0**.

1. On the **New SAML connection** page, click **Download metadata**.

## Configuring Azure Active Directory application
{: #connect_import_ad_cpd}
{: step}


Complete the [configuration steps](https://www.ibm.com/docs/en/cloud-paks/foundational-services/4.x_cd?topic=configuration-integrating-saml-azure-active-directory#configure-your-azure-active-directory-application-with-saml-sso__title__1) in the [Microsoft Azure portal](https://portal.azure.com/auth/login/) and save the Federation Metadata XML to your local drive.


## Upload the Federation Metadata XML configuration to watsonx.data on IBM Software Hub
{: #upload_import_ad_cpd}
{: step}

Complete these steps from watsonx.data on IBM Software Hub.

1. Log in to your console as an admin user.

1. Click **Identity providers**.

1. Edit the SAML connection that you created in [Retrieving the SAML metadata file from your watsonx.data on IBM Software Hub](#connect_import_ad) section.

1. Click **Token attribute mapping**.

1. Update the token attribute-mapping fields such as Email, Family name, Given name, Groups abnd Sub from the Azure Active Directory Federation Metadata XML file that you downloaded in the Set up SSO section.

1. In the **From identity provider** section, upload the Federation Metadata XML file that you saved in [Configuring Azure Active Directory application](#connect_import_ad_cpd) section.

1. Click **Save**.




## Verify the configuration by testing the intergration
{: #upload_import_ad_cpd}
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
{: #verify_mask}
{: step}

1. Log in to IBM Knowledge Catalog.
1. From the left pane, go to **Governance** > **Rules**.
1. From the **Rules** page, verify that the rules corresponding to your data class of the column is defined. You can define a new rule by using **Add rule** button.

The owner can see the unmasked data. To verify whether masking is functioning correctly, log in to {{site.data.keyword.lakehouse_short}} as user who is not the owner of the asset in IKC and query the asset.
{: note}
