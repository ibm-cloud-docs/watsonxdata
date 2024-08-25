---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-25"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Resource group properties
{: #resource_grp_pptys}

You can format the resource group JSON file to match with the sample resource group file that you can download from the console.
{: shortdesc}

The following sections cover the resource group properties that you can configure.

## Main properties
{: #main_pptys}

| Property name | Type | Required/Optional | Description |
| --- | --- | --- | --- |
| [`rootGroups`](#rootGroups_pptys) | Array | Required | Defines the specifications for resource groups. |
| [`selectors`](#selectors_pptys) | Array | Required | Specifies the selector configurations for the resource groups. |
| [`cpuQuotaPeriod`](#cpuQuotaPeriod_prpty) | String | Optional | Specifies the CPU quota period. This property must match with the pattern `^\d+(.\d+)?[smhd]$`. |
{: caption="Table 1. Main properties" caption-side="bottom"}

## `rootGroups` properties
{: #rootGroups_pptys}

| Property name | Type | Required/Optional | Description |
| --- | --- | --- | --- |
| `name` | String | Required | Name of the resource group. If the name contains `{`, `}`, or `$`, the name must be in the pattern `\$\{([a-zA-Z][a-zA-Z0-9]*)\}`. Blank spaces are allowed in the name. The name cannot contain a period (.). You cannot have the same name for two sibling groups. You can have the same name for a root group and a sub group. |
| `softMemoryLimit` | String | Required | Specifies the soft memory limit. Minimum value: 0%. Maximum value: 999%. |
| `maxQueued` | Integer | Optional | Specifies the maximum number of queued requests. Minimum value: 0. Maximum value: 2147483647. The value must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value. |
| `softConcurrencyLimit` | Integer or null | Optional | Specifies the soft concurrency limit. Minimum value: 0. Maximum value: 2147483647. The value must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value. |
| `maxRunning` | Integer or null | Optional | Specifies the maximum running count. Minimum value: 0. Maximum value: 2147483647. The value must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value.|
| `hardConcurrencyLimit` | Integer | Required (If `maxRunning` value is available, `hardConcurrencyLimit` takes up that value. If `maxRunning` is not set, you must set a value for `hardConcurrencyLimit`.) | Specifies the hard concurrency limit. Minimum value: 0. Maximum value: 2147483647. The value must be greater than or equal to `softConcurrencyLimit`. It must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value. |
| `schedulingPolicy` | String (Following are the available values: `fair`, `weighted`, `weighted_fair`, `query_priority`. These values are not case-sensitive.) | Optional | Specifies the scheduling policy. |
| `schedulingWeight` | Integer or null | Optional | Specifies the scheduling weight. Allowed values (minimum to maximum): 1 to 2147483647. The value must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value. If a subgroup has `schedulingWeight`, all of the corresponding siblings in that subgroup must have `schedulingWeight`. |
| `subGroups` | Array or null | Optional | Specifies the subgroups within the resource group. Subgroups have the same rules for different properties as in the resource group. |
| `jmxExport` | Boolean or null | Optional | Indicates whether JMX export is enabled. |
| `softCpuLimit` | String | Optional | Specifies the soft CPU limit. It must match the pattern `^\d+(.\d+)?[smhd]$`. If `hardCpuLimit` is defined, the value of `softCpuLimit` must be less than or equal to `hardCpuLimit`. |
| `hardCpuLimit` | String | Optional | Specifies the hard CPU limit. It must match the pattern `^\d+(\.\d+)?[smhd]$`. |
| `perQueryLimits` | Object | Optional | Specifies per-query limits. Example: `"perQueryLimits": { "executionTimeLimit": "30m", "totalMemoryLimit": "2GB", "cpuTimeLimit": "1h" }`. The object can have one, two, or three of the following limits. Negative values are not allowed for any of the following limits. 1. `executionTimeLimit` (**Type**: String, **Pattern**: This property must match with the pattern `^\d+(.\d+)?[smhd]$`.), 2. `totalMemoryLimit` (**Type**: String, **Pattern**: This property must match with the pattern `^\s*(\d+(?:\.\d+)?)\s*([a-zA-Z]+)\s*$`.), 3. `cpuTimeLimit` (**Type**: String, **Pattern**: This property must match with the pattern `^\d+(.\d+)?[smhd]$`.) |
| `workersPerQueryLimit` | Integer or null | Optional | Specifies the workers per query limit. Allowed values (minimum to maximum): -2147483648 to 2147483647. The value must be greater than or equal to `softConcurrencyLimit`. It must not start with `0`. For example, `01`, `05`. Specify the values as `1`, `5`. `0` alone is a valid value. |
{: caption="Table 2. rootGroups properties" caption-side="bottom"}

## `selectors` properties
{: #selectors_pptys}

| Property name | Type | Required/Optional | Description |
| --- | --- | --- | --- |
| `user` | String or null (Strings can have any valid regular expression (`.*`).) | Optional | Specifies the user regex pattern. |
| `source` | String or null (Strings can have any valid regular expression (`.*`).) | Optional | Specifies the source regex pattern. |
| `queryType` | String or null. (Possible values are `data_definition`, `delete`, `describe`, `explain`, `analyze`, `insert`, `select`, `control`, and `update`. These values are not case-sensitive.) | Optional | Specifies the query type. |
| `clientTags` | List of strings or null (Example: `"clientTags": ["resourceGroup1","resourceGroup2"]`. storageStrings can have any valid regular expression (`.*`).) | Optional | Specifies the client tags. |
| `selectorResourceEstimate` | Object or null | Optional | Specifies the selector resource estimate. Example: "selectorResourceEstimate": `{"executionTime": {"min": "5m", "max": "10m"}, "cpuTime": {"min": "30m", "max": "1h"}, "peakMemory": {"min": "512MB", "max": "2GB"}`. The object can have one, two, or three of the limits. You can also use the `min`, `max`, or both of the parameters for all of the three limits. For example, `"selectorResourceEstimate": {"executionTime": {"min": "5m"}`. Negative values are not allowed for any of the limits. For more information about the limits, see [`selectorResourceEstimate` limits](#selectorResourceEstimate_limits). |
| `clientInfo` | String or null (Strings can have any valid regular expression (`.*`).) | Optional | Specifies the client info regex pattern. |
| `schema` | String or null (Strings can have any valid regular expression (`.*`).) | Optional | Specifies the schema. |
| `principal` | String or null (Strings can have any valid regular expression (`.*`).) | Optional | Specifies the principal regex pattern. |
| `group` | String | Required | The group name must be from the available names in the resource group. For redirecting to a subgroup, use `"group": "groupname.subgroupname"`. You can also use dynamic values like `${SOURCE}`, `${USER}`, and `${SCHEMA}` as used in root group names. You cannot have `null` in `group`. |
{: caption="Table 3. selectors properties" caption-side="bottom"}

In the `source` and `user` regex, you can use the provided name in the format `(?<sampleName>.*)` as a dynamic group name. For example:

```bash
{
            "source": "(?<sampleName>.*)",
            "clientTags": [
                "hipri"
            ],
            "group": "bi-${sampleName}"
}and there is a group as ,{
            "name": "bi-${sampleName}",
            "softMemoryLimit": "80%",
            "hardConcurrencyLimit": 100,
            "maxQueued": 1000,
            "schedulingPolicy": "weighted",
            "jmxExport": true
}
```
{: codeblock}

In this example, `sampleName` is a dynamic value. Special characters are not allowed in the name. You can add other values like `${SOURCE}`, `${USER}`, or `${SCHEMA}`. The group name is case-sensitive. You can have values before and after the dynamic variable. For example, `abc-${SOURCE}` or `${toolname}-xyz`.


### `selectorResourceEstimate` limits
{: #selectorResourceEstimate_limits}

- `executionTime`
    - `min`:
      The property type is string. This property must match the pattern `^\\d+(\\.\\d+)?[smhd]$`.
    - `max`:
      The property type is string. This property must match the pattern  `^\\d+(\\.\\d+)?[smhd]$`.

- `peakMemory`
    - `min`:
        The property type is string. This property must match the pattern `^\s*(\d+(?:\.\d+)?)\s*([a-zA-Z]+)\s*$`.
   - `max`
        The property type is string. This property must match the pattern `^\s*(\d+(?:\.\d+)?)\s*([a-zA-Z]+)\s*$`.

- `cpuTime`
    - `min`:
      The property type is string. This property must match the pattern `^\\d+(\\.\\d+)?[smhd]$`.
    - `max`:
      The property type is string. This property must match the pattern  `^\\d+(\\.\\d+)?[smhd]$`.

## cpuQuotaPeriod properties
{: #cpuQuotaPeriod_prpty}

| Property name | Type   | Required/Optional | Description |
|---------------|--------|-------------------|-------------|
| cpuQuotaPeriod | String | Optional | Specifies the CPU quota period. This property must match with the pattern `^\\d+(\\.\\d+)?[smhd]$` |
{: caption="Table 4. selectors properties" caption-side="bottom"}
