---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-29"

keywords: lakehouse, bucket, catalog, watsonx.data

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


# Setting up GlusterFS replicated storage with MinIO
{: #setting_glusterfs}

You can integrate GlusterFS with MinIO in watsonx.data when using it as your storage backend.

## Before you begin
{: #setting_glusterfs_pre}

You must have **Virtual Machines (VM)** with static IPs and hostname resolution configured.

### Roles
{: #setting_glusterfs_rol}

| Node | Role                          |
|------|-------------------------------|
| VM1  | GlusterFS Client (MinIO Host) |
| VM2  | GlusterFS Server              |
| VM3  | GlusterFS Server              |

## Procedure
{: #setting_glusterfs_pro}

Complete the following steps to set up GlusterFS replicated storage with MinIO.

1. Run the following command on all nodes (VMs) to install GlusterFS.

   ```bash
    dnf install centos-release-gluster -y
    dnf module enable glusterfs -y
    dnf install glusterfs-server -y
    
    systemctl start glusterd.service
    systemctl status glusterd.service
    ```
    {: codeblock}

2. Run the following command on VM2 and VM3 to create brick directory on server nodes.

   ```bash
   <ip-of-vm1> vm1.fyre.ibm.com
   <ip-of-vm2> vm2.fyre.ibm.com
   <ip-of-vm3> vm3.fyre.ibm.com
   ```
   {: codeblock}

3. Run the following command on VM2 and VM3 to create brick directory on server nodes.
   ```bash
   mkdir -p /gluster-brick/data
   ```
   {: codeblock}

4. Run the following command on VM2 to probe peers from a server node.

   ```bash
   gluster peer probe vm3.fyre.ibm.com
   gluster peer status
   ```
   {: codeblock}

5. Run the following command on VM2 to create Gluster volume.

   ```bash
   gluster volume create gv0 replica 2 vm2.fyre.ibm.com:/gluster-brick/data vm3.fyre.ibm.com:/gluster-brick/data force
   gluster volume start gv0
   ```
   {: codeblock}

6. Run the following command on VM1 to create Gluster volume on client.

   ```bash
   mkdir -p /mnt/gluster-data
   mount -t glusterfs vm2.fyre.ibm.com:/gv0 /mnt/gluster-data
   ```
   {: codeblock}

7. Run the following command on VM1 to verify Gluster replication on client.

   ```bash
   echo "Test file from client" > /mnt/gluster-data/test.txt
   ```
   {: codeblock}

8. Run the following command on VM2 and VM3 to verify Gluster replication on servers.

   ```bash
   ls /gluster-brick/data/test.txt
   ```
   {: codeblock}

9. Download the MinIO binary and place it in `/usr/local/bin/`, then run the following command.

   ```bash
   export MINIO_ROOT_USER=minioadmin
   export MINIO_ROOT_PASSWORD=minioadmin
   export MINIO_CONSOLE_ADDRESS=":9001"
   nohup minio server /mnt/gluster-data --address ":9000" > minio.log 2>&1 &
   ```
   {: codeblock}

10. Open the following URL in your web browser.

   ```bash
   http://:9001
   ```
   {: codeblock}

    {%- capture gluster -%}
   <md-block>

    **Login credentials:**
    
    - **Username**: `minioadmin`
    - **Password**: `minioadmin`

   </md-block>
   {%- endcapture %}

   {% render "note.html", type: "note", text: gluster %}

11. Create a storage, and upload a file.
12. Run the following command on VM2 and VM3 to verify file replication on storage nodes.

   ```bash
   ls /gluster-brick/data
   ```
   {: codeblock}

   Make sure that you see the bucket directory and uploaded file replicated on both storage nodes.
   {: note}
