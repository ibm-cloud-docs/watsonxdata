---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-28"

keywords: lakehouse, watsonx.data, presto

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

# Monitoring Presto engine JMX metrics with Sysdig on {{site.data.keyword.cloud_notm}}
{: #monitor_metrics}

You can set up JMX metrics monitoring for your Presto pods on {{site.data.keyword.cloud_notm}} using Sysdig. With this monitoring setup, you can collect and visualize JMX metrics from your Presto instances.

To view the metrics, you must create an IBM Cloud Monitoring instance and enable it for platform metrics.

## Access your monitoring data
{: #access_monitoring_data}

To access your monitoring data, you must have a Sysdig instance running in your account.

1. Log in to your {{site.data.keyword.cloud_notm}} account and access the {{site.data.keyword.cloud_notm}} console.
1. In the left pane, go to **Observability** > **Monitoring** > **Instances**. You can see a list of entries for different regions.
1. Choose the region where your Presto cluster is located and click **Open dashboard** to open the Sysdig dashboard. On the Sysdig dashboard, you can either browse through or search for specific metrics that use the instance ID.
1. Expand the cluster name to reveal the instance ID associated with your Presto instances.
1. Expand the `pc` category to access a list of available metrics. `pc` represents Presto coordinators.
1. Select **watsonx** to see the available metrics.
1. Click a metric to view the graphical representations of the data, which makes it easy to monitor and analyze your Presto JMX metrics.

### Presto dashboard
{: #access_dashboard_presto}

From the left pane, click **Dashboards**. You can see two dashboards:

- **Presto** (general dashboard): You can find scheduler, CPU, query, and cache related metrics panels here.
- **Presto Memory Panel**: You can find heap, non-heap, and GC related metrics panels here.

For information about the Presto exposed JMX metrics details, see [Presto exposed JMX metrics](watsonxdata?topic=watsonxdata-presto_expd_jmx).

For cloud platforms other than {{site.data.keyword.cloud_notm}}, import and use the following dashboard on Grafana to get the pre-built panels for Presto.

```json
{
  "__inputs": [
    {
      "name": "DS_PROMETHEUS",
      "label": "Prometheus",
      "description": "",
      "type": "datasource",
      "pluginId": "prometheus",
      "pluginName": "Prometheus"
    }
  ],
  "__elements": [],
  "__requires": [
    {
      "type": "grafana",
      "id": "grafana",
      "name": "Grafana",
      "version": "8.4.7"
    },
    {
      "type": "datasource",
      "id": "prometheus",
      "name": "Prometheus",
      "version": "1.0.0"
    },
    {
      "type": "panel",
      "id": "timeseries",
      "name": "Time series",
      "version": ""
    }
  ],
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": "-- Grafana --",
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "target": {
          "limit": 100,
          "matchAny": false,
          "tags": [],
          "type": "dashboard"
        },
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "id": null,
  "iteration": 1698702275305,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 0
      },
      "id": 192,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 1
          },
          "id": 195,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "up{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} - {{kubernetes_pod_ip}}",
              "refId": "A"
            }
          ],
          "title": "Worker Status",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 1
          },
          "id": 194,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "up{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "Coordinator Status",
          "type": "timeseries"
        }
      ],
      "title": "Cluster Status",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 1
      },
      "id": 93,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 2
          },
          "id": 95,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_bytes_read_cache_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_bytes_read_cache_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_bytes_read_cache_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_bytes_read_cache_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache Bytes Read Rate",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 2
          },
          "id": 96,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_bytes_requested_external_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_bytes_requested_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_bytes_requested_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_bytes_requested_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache External Bytes Request Rate",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 24,
            "x": 0,
            "y": 9
          },
          "id": 97,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_written_cache_external_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_written_cache_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_written_cache_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_written_cache_external_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache External Bytes Written Rate",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 16
          },
          "id": 98,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_get_errors_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_get_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_get_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_get_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache Get Errors Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 16
          },
          "id": 99,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_put_errors_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_put_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_put_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_put_errors_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache Put Errors Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 23
          },
          "id": 100,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_pages_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_pages_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_pages_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_pages_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cached Pages",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 23
          },
          "id": 101,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_alluxio_cache_pages_evicted_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_alluxio_cache_pages_evicted_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_alluxio_cache_pages_evicted_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_alluxio_cache_pages_evicted_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cached Evicted Pages",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 30
          },
          "id": 102,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_alluxio_cache_space_available_value{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_alluxio_cache_space_available_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_alluxio_cache_space_available_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_alluxio_cache_space_available_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache Space Available",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 30
          },
          "id": 103,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_alluxio_cache_space_used_value{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_alluxio_cache_space_used_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_alluxio_cache_space_used_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_alluxio_cache_space_used_value{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Alluxio Cache Space Used",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 37
          },
          "id": 108,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_fragment_cache_stats_cache_entries{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_fragment_cache_stats_cache_entries{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_fragment_cache_stats_cache_entries{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_fragment_cache_stats_cache_entries{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Fragment Results Cache Entries",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 37
          },
          "id": 109,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_fragment_cache_stats_cache_hit{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_fragment_cache_stats_cache_hit{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_fragment_cache_stats_cache_hit{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_fragment_cache_stats_cache_hit{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Fragment Results Cache Hit Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 44
          },
          "id": 110,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_fragment_cache_stats_cache_removal{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_fragment_cache_stats_cache_removal{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_fragment_cache_stats_cache_removal{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_fragment_cache_stats_cache_hit{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Fragment Results Cache Removal Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 44
          },
          "id": 111,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Fragment Results Cache Size Bytes",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 6,
            "y": 51
          },
          "id": 112,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_fragment_cache_stats_inflight_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_fragment_cache_stats_inflight_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_fragment_cache_stats_inflight_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_fragment_cache_stats_inflight_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Fragment Results Cache Inflight Bytes",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 58
          },
          "id": 114,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Parquet Metadata Cache Hit Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 58
          },
          "id": 113,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Parquet Metadata Cache Size",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 65
          },
          "id": 115,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "ORC File Tail Cache Hit Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 65
          },
          "id": 116,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "ORC File Tail Cache Size",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 72
          },
          "id": 117,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_stripe_stream_hit_rate{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_stripe_stream_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_stripe_stream_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_stripe_stream_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Stripe Footer Cache Hit Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 72
          },
          "id": 118,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_cache_stats_mbean_stripe_footer_size{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_cache_stats_mbean_stripe_footer_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_cache_stats_mbean_stripe_footer_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_cache_stats_mbean_stripe_footer_size{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Stripe Footer Cache Size",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 24,
            "x": 0,
            "y": 79
          },
          "id": 119,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_caching_directory_lister_request_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_caching_directory_lister_request_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_caching_directory_lister_request_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_caching_directory_lister_request_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Directory Lister Cache Request Count",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 85
          },
          "id": 120,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Directory Lister Cache Hit Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 85
          },
          "id": 121,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_hive_caching_directory_lister_hit_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Directory Lister Cache Hit Count",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 92
          },
          "id": 122,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_caching_directory_lister_miss_rate{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Directory Lister Cache Miss Rate",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 92
          },
          "id": 123,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_hive_caching_directory_lister_hit_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_hive_caching_directory_lister_hit_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Directory Lister Cache Miss Count",
          "type": "timeseries"
        }
      ],
      "title": "Caching",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 2
      },
      "id": 125,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 6
          },
          "id": 183,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_hive_metastore_glue_aws_request_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_hive_metastore_glue_aws_request_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_hive_metastore_glue_aws_request_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_hive_metastore_glue_aws_request_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, rate(watsonx_data_presto_hive_metastore_glue_aws_request_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Glue AWS Request Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 6
          },
          "id": 190,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_hive_metastore_glue_aws_retry_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_hive_metastore_glue_aws_retry_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_hive_metastore_glue_aws_retry_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_hive_metastore_glue_aws_retry_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, rate(watsonx_data_presto_hive_metastore_glue_aws_retry_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Glue AWS Request Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 14
          },
          "id": 189,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_hive_metastore_glue_aws_throttle_exceptions_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_hive_metastore_glue_aws_throttle_exceptions_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_hive_metastore_glue_aws_throttle_exceptions_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_hive_metastore_glue_aws_throttle_exceptions_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, rate(watsonx_data_presto_hive_metastore_glue_aws_throttle_exceptions_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Glue AWS Request Count",
          "type": "timeseries"
        }
      ],
      "title": "Metastore",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 3
      },
      "id": 197,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 7
          },
          "id": 38,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Old Gen Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 7
          },
          "id": 77,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_old_gen_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Old Gen Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 0,
            "y": 13
          },
          "id": 54,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Old Gen Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 12,
            "y": 13
          },
          "id": 78,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_old_gen_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Old Gen Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 0,
            "y": 18
          },
          "id": 39,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "used - {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Young Gen Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 12,
            "y": 18
          },
          "id": 79,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "used - {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_eden_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Young Gen Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 0,
            "y": 23
          },
          "id": 55,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Young Gen Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 12,
            "y": 23
          },
          "id": 80,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_eden_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Young Gen Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 0,
            "y": 28
          },
          "id": 40,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Survivor Space Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 12,
            "y": 28
          },
          "id": 81,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_survivor_space_usage_used_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Survivor Space Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 0,
            "y": 33
          },
          "id": 56,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\",    presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\",    presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker JVM Survivor Space Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 5,
            "w": 12,
            "x": 12,
            "y": 33
          },
          "id": 82,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\",    presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator JVM Survivor Space Committed",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "GC Time (ms/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": [
              {
                "matcher": {
                  "id": "byRegexp",
                  "options": "Pause (.*)"
                },
                "properties": [
                  {
                    "id": "custom.axisPlacement",
                    "value": "right"
                  },
                  {
                    "id": "custom.axisLabel",
                    "value": "Pause Rate (ms/sec)"
                  },
                  {
                    "id": "custom.lineStyle",
                    "value": {
                      "dash": [
                        10,
                        10
                      ],
                      "fill": "dash"
                    }
                  }
                ]
              }
            ]
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 38
          },
          "id": 41,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_time_milliseconds{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[5m])",
              "interval": "",
              "legendFormat": "Old Gen GC Rate {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "1000 * rate(watsonx_data_presto_pause_meter_total_pause_seconds{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[5m])",
              "hide": false,
              "interval": "",
              "legendFormat": "Pause Rate {{kubernetes_pod_ip}}",
              "refId": "B"
            }
          ],
          "title": "Worker JVM Old Gen Collection Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "GC Time (ms/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": [
              {
                "matcher": {
                  "id": "byRegexp",
                  "options": "Pause (.*)"
                },
                "properties": [
                  {
                    "id": "custom.axisPlacement",
                    "value": "right"
                  },
                  {
                    "id": "custom.axisLabel",
                    "value": "Pause Rate (ms/sec)"
                  },
                  {
                    "id": "custom.lineStyle",
                    "value": {
                      "dash": [
                        10,
                        10
                      ],
                      "fill": "dash"
                    }
                  }
                ]
              }
            ]
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 38
          },
          "id": 83,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_time_milliseconds{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[5m])",
              "interval": "",
              "legendFormat": "Old Gen GC Rate {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "1000 * rate(watsonx_data_presto_pause_meter_total_pause_seconds{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[5m])",
              "hide": false,
              "interval": "",
              "legendFormat": "Pause Rate {{kubernetes_pod_ip}}",
              "refId": "B"
            }
          ],
          "title": "Coordinator JVM Old Gen Collection Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "Collection Rate (count/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 44
          },
          "id": 43,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker Old Gen Collection Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "Collection Rate (count/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 44
          },
          "id": 84,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_garbage_collector_g1_old_generation_collection_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator Old Gen Collection Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "GC Time (ms/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": [
              {
                "matcher": {
                  "id": "byRegexp",
                  "options": "Pause .*"
                },
                "properties": [
                  {
                    "id": "custom.axisPlacement",
                    "value": "right"
                  },
                  {
                    "id": "custom.axisLabel",
                    "value": "Pause Time (ms/sec)"
                  },
                  {
                    "id": "custom.lineStyle",
                    "value": {
                      "dash": [
                        10,
                        10
                      ],
                      "fill": "dash"
                    }
                  }
                ]
              }
            ]
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 50
          },
          "id": 42,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_time_milliseconds{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "Young Gen GC Rate {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "1000 * rate(watsonx_data_presto_pause_meter_total_pause_seconds{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "hide": false,
              "interval": "",
              "legendFormat": "Pause Rate {{kubernetes_pod_ip}}",
              "refId": "B"
            }
          ],
          "title": "Worker JVM Young Gen Collection Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "GC Time (ms/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": [
              {
                "matcher": {
                  "id": "byRegexp",
                  "options": "Pause .*"
                },
                "properties": [
                  {
                    "id": "custom.axisPlacement",
                    "value": "right"
                  },
                  {
                    "id": "custom.axisLabel",
                    "value": "Pause Time (ms/sec)"
                  },
                  {
                    "id": "custom.lineStyle",
                    "value": {
                      "dash": [
                        10,
                        10
                      ],
                      "fill": "dash"
                    }
                  }
                ]
              }
            ]
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 50
          },
          "id": 85,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_time_milliseconds{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "Young Gen GC Rate {{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "1000 * rate(watsonx_data_presto_pause_meter_total_pause_seconds{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "hide": false,
              "interval": "",
              "legendFormat": "Pause Rate {{kubernetes_pod_ip}}",
              "refId": "B"
            }
          ],
          "title": "Coordinator JVM Young Gen Collection Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "Collection Rate (#/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 56
          },
          "id": 44,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Worker Young Gen Collection Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "Collection Rate (#/sec)",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 56
          },
          "id": 86,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[1m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_garbage_collector_g1_young_generation_collection_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[1m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Coordinator Young Gen Collection Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 62
          },
          "id": 143,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-worker\",    presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker JVM Native Memory Used",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 62
          },
          "id": 144,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_memory_heap_memory_usage_max_bytes{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"} - (watsonx_data_presto_memory_heap_memory_usage_used_bytes + watsonx_data_presto_memory_non_heap_memory_usage_used_bytes + watsonx_data_presto_java_nio_buffer_pool_direct_memory_used))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_memory_pool_g1_survivor_space_usage_committed_bytes{presto_cluster_app=\"presto-coordinator\",    presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator JVM Native Memory Used",
          "type": "timeseries"
        }
      ],
      "title": "GC Stats",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 4
      },
      "id": 105,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 9
          },
          "id": 146,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Active Connections",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 9
          },
          "id": 147,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_active_connections_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Active Connections",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 17
          },
          "id": 148,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Started Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 17
          },
          "id": 149,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_started_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Started Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 25
          },
          "id": 150,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Failed Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 25
          },
          "id": 151,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Failed Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 33
          },
          "id": 152,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Successful Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 33
          },
          "id": 153,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Successful Uploads",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 41
          },
          "id": 154,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Metadata Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 41
          },
          "id": 155,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_metadata_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Metadata Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 49
          },
          "id": 156,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 List Status Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 49
          },
          "id": 157,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 List Status Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": [
              {
                "__systemRef": "hideSeriesFrom",
                "matcher": {
                  "id": "byNames",
                  "options": {
                    "mode": "exclude",
                    "names": [
                      "10.128.20.55 - eventglue"
                    ],
                    "prefix": "All except:",
                    "readOnly": true
                  }
                },
                "properties": [
                  {
                    "id": "custom.hideFrom",
                    "value": {
                      "legend": false,
                      "tooltip": false,
                      "viz": true
                    }
                  }
                ]
              }
            ]
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 57
          },
          "id": 158,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 List Located Status Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 57
          },
          "id": 159,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_located_status_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 List Located Status Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 65
          },
          "id": 160,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 List Objects Status Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 65
          },
          "id": 175,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_list_objects_calls_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 List Objects Calls",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 73
          },
          "id": 161,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Other Read Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 73
          },
          "id": 176,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Other Read Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 81
          },
          "id": 162,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 AWS Aborted Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 81
          },
          "id": 177,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_aws_aborted_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 AWS Aborted Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 89
          },
          "id": 164,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Socket Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 89
          },
          "id": 178,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Socket Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 97
          },
          "id": 166,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Socket Timeout Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 97
          },
          "id": 179,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Socket Timeout Exceptions",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 105
          },
          "id": 168,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Get Object Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 105
          },
          "id": 180,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Get Object Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 113
          },
          "id": 170,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Get Metadata Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 113
          },
          "id": 181,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Get Metadata Errors",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 121
          },
          "id": 172,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Get Object Retries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 121
          },
          "id": 182,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Get Object Retries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 129
          },
          "id": 184,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Get Metadata Retries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 129
          },
          "id": 185,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_one_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator S3 Get Metadata Retries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 137
          },
          "id": 174,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Read Retries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 137
          },
          "id": 188,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}} - {{catalog_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_one_minute_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker S3 Read Retries",
          "type": "timeseries"
        }
      ],
      "title": "IO",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 5
      },
      "id": 22,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 5
          },
          "id": 209,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_cluster_memory_manager_queries_killed_due_to_out_of_memory{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "Queries Killed Due to OOM",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 5
          },
          "id": 210,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_cluster_memory_pool_general_assigned_queries{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "General Pool Assigned Queries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 13
          },
          "id": 211,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_cluster_memory_pool_general_blocked_nodes{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "General Pool Blocked Nodes",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "percentunit"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 13
          },
          "id": 212,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_cluster_memory_pool_general_free_distributed_bytes{presto_cluster_name=~\"$cluster_name\"} / watsonx_data_presto_cluster_memory_pool_general_total_distributed_bytes",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "% Free General Pool Distributed Bytes",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 21
          },
          "id": 6,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\", area=\"heap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"heap\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\",})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.90, jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\",})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "E"
            }
          ],
          "title": "Worker JVM Committed Heap",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 21
          },
          "id": 73,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", area=\"heap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"heap\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.90, jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "E"
            }
          ],
          "title": "Coordinator JVM Committed Heap",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 0,
            "y": 27
          },
          "id": 71,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$worker_pod_selector\", area=\"nonheap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"nonheap\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.90, jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_committed{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "E"
            }
          ],
          "title": "Worker JVM Committed Nonheap",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 6,
            "w": 12,
            "x": 12,
            "y": 27
          },
          "id": 74,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", area=\"nonheap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", kubernetes_pod_ip=~\"$quantiles\", presto_cluster_name=~\"$cluster_name\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.90, jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_committed{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "E"
            }
          ],
          "title": "Coordinator JVM Committed Nonheap",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 33
          },
          "id": 37,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\", area=\"heap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker JVM Heap Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 33
          },
          "id": 75,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\", area=\"heap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$quantiles\", area=\"heap\", presto_cluster_name=~\"$cluster_name\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"heap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator JVM Heap Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 40
          },
          "id": 72,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\", area=\"nonheap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, jvm_memory_bytes_used{presto_cluster_app=\"presto-worker\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker JVM Nonheap Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 40
          },
          "id": 76,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\", area=\"nonheap\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, jvm_memory_bytes_used{presto_cluster_app=\"presto-coordinator\", area=\"nonheap\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator JVM Nonheap Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 47
          },
          "id": 138,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker Direct Buffer Pool Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 47
          },
          "id": 137,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator Direct Buffer Pool Count",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 54
          },
          "id": 139,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker Direct Buffer Pool Total Capacity",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 54
          },
          "id": 140,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_total_capacity{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator Direct Buffer Pool Total Capacity",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 61
          },
          "id": 141,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-worker\", kubernetes_pod_ip=~\"$worker_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "hide": false,
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Worker Direct Buffer Pool Used",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 61
          },
          "id": 142,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.9, watsonx_data_presto_java_nio_buffer_pool_direct_memory_used{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p90",
              "refId": "E"
            }
          ],
          "title": "Coordinator Direct Buffer Pool Used",
          "type": "timeseries"
        }
      ],
      "title": "Memory Usage",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 6
      },
      "id": 199,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 24,
            "x": 0,
            "y": 6
          },
          "id": 203,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_cluster_memory_manager_cluster_memory_bytes{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "Cluster Memory",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 14
          },
          "id": 201,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_cluster_memory_manager_cluster_user_memory_reservation{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "Cluster User Memory Reservation",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 14
          },
          "id": 202,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_memory_cluster_memory_manager_cluster_total_memory_reservation{presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "A"
            }
          ],
          "title": "Cluster Total Memory Reservation",
          "type": "timeseries"
        }
      ],
      "title": "Cluster Memory",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 7
      },
      "id": 26,
      "panels": [
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 11,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "normal"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 7
          },
          "id": 2,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "multi",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_abandoned_queries_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "interval": "",
              "legendFormat": "abandoned - {{presto_cluster_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_canceled_queries_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "cancelled - {{presto_cluster_name}}",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_insufficient_resources_failures_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "insufficient resources - {{presto_cluster_name}}",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_internal_failures_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "internal failure - {{presto_cluster_name}}",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_external_failures_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "external error - {{presto_cluster_name}}",
              "refId": "E"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_user_error_failures_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "user error - {{presto_cluster_name}}",
              "refId": "G"
            }
          ],
          "title": "Failed Queries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 7
          },
          "id": 4,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(avg_over_time(watsonx_data_presto_query_manager_running_queries{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[1m])) by (presto_cluster_name)",
              "interval": "",
              "legendFormat": "running_queries - {{presto_cluster_name}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(avg_over_time(watsonx_data_presto_query_manager_queued_queries{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[1m])) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "queued - {{presto_cluster_name}}",
              "refId": "B"
            }
          ],
          "title": "Running Queries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 0,
            "y": 15
          },
          "id": 136,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(avg_over_time(watsonx_data_presto_query_manager_queued_queries{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}[1m])) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "queued - {{presto_cluster_name}}",
              "refId": "B"
            }
          ],
          "title": "Submitted Queries",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              }
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 12,
            "x": 12,
            "y": 15
          },
          "id": 204,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_consumed_cpu_time_seconds_five_minute_count{presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "queued - {{presto_cluster_name}}",
              "refId": "B"
            }
          ],
          "title": "Consumed CPU Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "ms"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 8,
            "w": 24,
            "x": 0,
            "y": 23
          },
          "id": 207,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_queued_time_five_minutes_p50{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_queued_time_five_minutes_p75{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p75",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_queued_time_five_minutes_p90{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p90",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_queued_time_five_minutes_p99{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p99",
              "refId": "E"
            }
          ],
          "title": "Queued Query Time",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 31
          },
          "id": 61,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p50{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p50",
              "refId": "D"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p75{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p75",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p90{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p90",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p95{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p95",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p99{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p99",
              "refId": "E"
            }
          ],
          "title": "Coordinator CPU Input Bytes Rate",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 31
          },
          "id": 14,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p50{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p75{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p75",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p90{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p90",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p99{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p99",
              "refId": "E"
            }
          ],
          "title": "Coordinator Wall Input Bytes Rate",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "decbytes"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 38
          },
          "id": 205,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum(watsonx_data_presto_query_manager_consumed_input_rows_five_minute_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}}",
              "refId": "D"
            }
          ],
          "title": "Coordinator Consumed Input Rows",
          "type": "timeseries"
        },
        {
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 38
          },
          "id": 206,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_execution_time_five_minutes_p50{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p50",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_execution_time_five_minutes_p75{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p75",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_execution_time_five_minutes_p90{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p90",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "sum (watsonx_data_presto_query_manager_execution_time_five_minutes_p99{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$coordinator_pod_selector\"}) by (presto_cluster_name)",
              "hide": false,
              "interval": "",
              "legendFormat": "{{presto_cluster_name}} p99",
              "refId": "E"
            }
          ],
          "title": "Coordinator Query Execution Time",
          "type": "timeseries"
        }
      ],
      "title": "Query Stats",
      "type": "row"
    },
    {
      "collapsed": true,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 8
      },
      "id": 107,
      "panels": [
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 9
          },
          "id": 127,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Non-Preferred Node Selected Count",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 12,
            "y": 9
          },
          "id": 128,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}[3m])",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, rate(watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count{presto_cluster_app=\"presto-coordinator\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"}[3m]))",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Non-Primary Preferred Node Selected Count",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palette-classic"
              },
              "custom": {
                "axisLabel": "",
                "axisPlacement": "auto",
                "barAlignment": 0,
                "drawStyle": "line",
                "fillOpacity": 0,
                "gradientMode": "none",
                "hideFrom": {
                  "legend": false,
                  "tooltip": false,
                  "viz": false
                },
                "lineInterpolation": "linear",
                "lineWidth": 1,
                "pointSize": 5,
                "scaleDistribution": {
                  "type": "linear"
                },
                "showPoints": "auto",
                "spanNulls": false,
                "stacking": {
                  "group": "A",
                  "mode": "none"
                },
                "thresholdsStyle": {
                  "mode": "off"
                }
              },
              "mappings": [],
              "thresholds": {
                "mode": "absolute",
                "steps": [
                  {
                    "color": "green"
                  },
                  {
                    "color": "red",
                    "value": 80
                  }
                ]
              },
              "unit": "none"
            },
            "overrides": []
          },
          "gridPos": {
            "h": 7,
            "w": 12,
            "x": 0,
            "y": 16
          },
          "id": 130,
          "options": {
            "legend": {
              "calcs": [],
              "displayMode": "list",
              "placement": "bottom"
            },
            "tooltip": {
              "mode": "single",
              "sort": "none"
            }
          },
          "targets": [
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_five_minute_rate{presto_cluster_app=\"presto-coordinator\", kubernetes_pod_ip=~\"$coordinator_pod_selector\", presto_cluster_name=~\"$cluster_name\"}",
              "interval": "",
              "legendFormat": "{{kubernetes_pod_ip}}",
              "refId": "A"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "min(watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_five_minute_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "min",
              "refId": "B"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "max(watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_five_minute_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "max",
              "refId": "C"
            },
            {
              "datasource": {
                "type": "prometheus",
                "uid": "${DS_PROMETHEUS}"
              },
              "exemplar": true,
              "expr": "quantile(0.5, watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_five_minute_rate{presto_cluster_app=\"presto-worker\", presto_cluster_name=~\"$cluster_name\", kubernetes_pod_ip=~\"$quantiles\"})",
              "hide": false,
              "interval": "",
              "legendFormat": "p50",
              "refId": "D"
            }
          ],
          "title": "Preferred Node Selected Count",
          "type": "timeseries"
        },
        {
          "description": "",
          "fieldConfig": {
            "defaults": {
              "color": {
                "mode": "palett
```
{: codeblock}
