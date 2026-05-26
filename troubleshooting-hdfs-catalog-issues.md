---

copyright:
  years: 2022, 2025
lastupdated: "2026-05-13"

keywords: watsonxdata, troubleshoot, case sensitivity

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

# Troubleshooting HDFS catalog errors
{: #troubleshooting-hdfs-catalog-issues}

The following issues might occur when creating an HDFS catalog in watsonx.data.

## General configuration requirements
{: #hdfs-general-config-requirements}

Before troubleshooting specific errors, ensure the following configuration requirements are met:

1. **Use Service Principals**: Always use Kerberos service principals for Hive and HDFS instead of user principals.

2. **Hive Metastore Port**: Use the Hive metastore port (typically `9083`) for the thrift port field.

3. **Network Access**: If the server is behind network access controls, ensure the following ports are accessible to the client:
   - Port `9083` (Hive Metastore)
   - Port `10000` (HiveServer2)
   - Port `8020` (HDFS NameNode)

## Kerberos connection timeout
{: #hdfs-kerberos-connection-timeout}

When you try to establish a connection with HDFS catalog, you might encounter a Kerberos connection timeout error.

```bash
Caused by: com.google.common.util.concurrent.UncheckedExecutionException:
java.lang.RuntimeException: javax.security.auth.login.LoginException: Connect timed out
```

### Why it's happening
{: #hdfs-kerberos-timeout-why}

This error typically occurs due to:
- Malformed Kerberos configuration files
- Unreachable Key Distribution Center (KDC)

### How to fix it
{: #hdfs-kerberos-timeout-fix}

1. Ensure the KDC server is properly specified in the `krb5.conf` file.

2. Use telnet to verify connectivity to the KDC server on port 88:

   ```bash
   telnet <kdc-server> 88
   ```
   {: codeblock}

3. Check that all Kerberos configuration files are correctly formatted and contain valid entries.

## HDFS/Hive service unreachable
{: #hdfs-hive-service-unreachable}

When you try to establish a connection with HDFS catalog, you might encounter an error indicating that the HDFS or Hive service is unreachable.

```bash
Suppressed: java.lang.RuntimeException: javax.security.auth.login.LoginException: Connect timed out
    ... 74 more
Caused by: javax.security.auth.login.LoginException: Connect timed out
    at jdk.security.auth/com.sun.security.auth.module.Krb5LoginModule.attemptAuthentication(Krb5LoginModule.java:789)
    at jdk.security.auth/com.sun.security.auth.module.Krb5LoginModule.login(Krb5LoginModule.java:597)
    ...
Caused by: java.net.SocketTimeoutException: Connect timed out
```

### Why it's happening
{: #hdfs-service-unreachable-why}

The HDFS or Hive service is unreachable from the client machine.

### How to fix it
{: #hdfs-service-unreachable-fix}

1. Confirm that the HDFS and Hive services are running on the target cluster.

2. Verify that the client machine can reach the HDFS and Hive services:
   ```bash
   telnet <hdfs-host> 8020
   telnet <hive-host> 9083
   ```
   {: codeblock}

3. Ensure no firewall rules are blocking access to the required ports.

4. Verify that the client machine has proper network routing to the cluster.


## No route to host
{: #hdfs-no-route-to-host}

When you try to establish a connection with HDFS catalog, you might encounter a "No route to host" error.

```bash
java.net.NoRouteToHostException: No route to host
```

### Why it's happening
{: #hdfs-no-route-why}

The watsonx.data validator pod cannot establish TCP connections to the Cloudera cluster on required ports (8020 for HDFS and 9083 for Hive Metastore).

### How to fix it
{: #hdfs-no-route-fix}

1. Open the required firewall ports on the Cloudera cluster:

   ```bash
   sudo firewall-cmd --permanent --add-port=8020/tcp
   sudo firewall-cmd --permanent --add-port=9083/tcp
   sudo firewall-cmd --reload
   ```
   {: codeblock}

2. After applying the firewall rules, test connectivity from the client:

   ```bash
   telnet <cluster-host> 8020
   telnet <cluster-host> 9083
   ```
   {: codeblock}

## SASL protection layer mismatch
{: #hdfs-sasl-protection-mismatch}

When you try to establish a connection with HDFS catalog, you might encounter a SASL protection layer mismatch error.

```bash
javax.security.sasl.SaslException: No common protection layer between client and server
```

### Why it's happening
{: #hdfs-sasl-why}

The client (watsonx.data) and server (Cloudera) have incompatible Kerberos RPC protection settings. The client is configured for `authentication` while the server requires `privacy`.

Hadoop RPC protection has three levels:
- **authentication**: Authentication only
- **integrity**: Authentication + checksums
- **privacy**: Authentication + checksums + encryption

Both client and server must use the same protection level.

### How to fix it
{: #hdfs-sasl-fix}

Update the `core-site.xml` file to match the server's protection level.

Locate the configuration (typically around line 15):

**Before:**

```bash
<property>
  <name>hadoop.rpc.protection</name>
  <value>authentication</value>
</property>
```

**After:**

```bash
<property>
  <name>hadoop.rpc.protection</name>
  <value>privacy</value>
</property>
```

If your Cloudera cluster is configured with `privacy` for maximum security, ensure the client configuration matches this setting.
{: note}
