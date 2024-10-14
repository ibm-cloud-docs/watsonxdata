---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-10"

keywords: lakehouse, watsonx data, iam, access, role

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}



# Managing IAM access for {{site.data.keyword.lakehouse_short}}
{: #iam}

{{site.data.keyword.cloud}} Identity and Access Management (IAM) controls access to {{site.data.keyword.lakehouse_full}} service instances for users in your account. Every user that accesses the {{site.data.keyword.lakehouse_short}} service in your account must be assigned an access policy with an IAM role.
{: shortdesc}

Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.lakehouse_short}}.

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. After you define the scope of the access policy, you assign a role.

Platform management roles enable users to perform tasks on service resources at the platform level.
For more information about platform management roles, see [Platform management roles](/docs/account?topic=account-userroles#platformroles).
For more information about IAM access, see [IAM access](/docs/account?topic=account-userroles).

The following table describes the privileges that you can assign to platform management roles and associated permissions for {{site.data.keyword.lakehouse_short}} service:

## {{site.data.keyword.lakehouse_short}} formation
{: #formation_role}

| Privileges | Administrator | User |
|--------------------------|----------------|--------|
| Create Presto engine | Y | N |
| Delete Presto engine | Y | N |
| Restart the internal HMS | Y | N |
| Scale the Presto engines| Y | N |
| Scale the internal HMS | Y | N |
| Unregister own or an external bucket | Y | N |
| Unregister any database  | Y | N |
| Activate cataloged buckets (restart HMS) | Y | N |
| Register own buckets | Y | Y |
| Unregister own buckets | Y | Y |
| Register own databases | Y | Y |
| Unregister own databases | Y | Y |
{: caption="Roles and privileges for {{site.data.keyword.lakehouse_short}} formation" caption-side="bottom"}

## Platform access roles
{: #platform_access_role}

Following are the {{site.data.keyword.cloud}} IAM platform management roles.

### User roles
{: #user_roles}

- Viewer
- Operator
- Editor

### Administrator roles
{: #admin_roles}

- Administrator

The **Service Configuration Reader** and **Key Manager** roles are not relevant for {{site.data.keyword.lakehouse_short}}.
{: note}

## Service access roles
{: #platform_access_role}

Following are the service access roles:

- MetadataAdmin: External users with read and write access to the metadata through Thrift APIs in {{site.data.keyword.lakehouse_short}}.
- DataAccess: Only supports IKC-{{site.data.keyword.lakehouse_short}} service-to-service authorization to profile data in {{site.data.keyword.lakehouse_short}}.
- MetastoreView: External users with read access to the metadata through HMS REST APIs in {{site.data.keyword.lakehouse_short}}.
