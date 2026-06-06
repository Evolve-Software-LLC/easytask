---
description: Datadog integration for EasyTask enables automated metric submission, event posting, and monitor creation directly from scheduled workflows.
keywords:
  - Datadog monitoring automation
  - metric scheduling
  - alert management
  - EasyTask Datadog integration
---

# Datadog API

The Datadog API provides a set of endpoints for submitting metrics, posting events, and creating monitors. It helps users track, analyze, and alert on their application and infrastructure performance.

## Why Integrate Datadog with EasyTask?

Datadog is a leading cloud monitoring and analytics platform used by engineering teams worldwide. By integrating Datadog with EasyTask, your scheduled tasks can automatically submit custom metrics, post events, and create monitors without manual intervention. This integration is ideal for SLO tracking, anomaly alerting, and automated incident response — ensuring your observability pipeline stays up to date as your workflows run on schedule.

## Required Values in Vault

```
"secret": {
    "api_key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "app_key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "host_url": "https://us5.datadoghq.com",
    "proxy_url": "http://10.0.21.254:3128"
}
```

## Example Usage

=== "Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integration": "datadog",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "datadog/secret"
        },
        "action": [
            {"submit_metrics":{
                "metric_name":"skyler.test",
                "metric_intake_type": 0,
                "tags": ["method:test, custom:metric"],
                "points": [{"timestamp": 1716704577, "value": 0.1},
                        {"timestamp": 1716704567, "value": 0.5},
                        {"timestamp": 1716704557, "value": 0.7},
                        {"timestamp": 1716704547, "value": 0.4},
                        {"timestamp": 1716704537, "value": 0.6}]
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    {
        "integration": "datadog",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "datadog/secret"
        },
        "error": false,
        "action": [
            {"submit_metrics": {"errors": []}
        ]
    }
    ```

## Functions

#### `submit_metrics`

**submit_metrics**: This function submits multiple metric points to the Datadog monitoring system, allowing users to track and analyze time-series data. It returns a dictionary containing confirmation of the submitted metrics.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | metric_name | str | Name of the metric to be submitted | yes |
    | metric_intake_type | int | Type of metric intake (e.g., 0 for gauge) | yes |
    | tags | list | List of tags associated with the metric | yes |
    | points | list | List of dictionaries containing timestamp and value pairs | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains confirmation of the submitted metrics, including success status and any errors |

=== "JSON"

    ```json
    {
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integration": "datadog",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "datadog/secret"
        },
        "action": [
            {"submit_metrics":{
                "metric_name":"skyler.test",
                "metric_intake_type": 0,
                "tags": ["method:test, custom:metric"],
                "points": [{"timestamp": 1716704577, "value": 0.1},
                        {"timestamp": 1716704567, "value": 0.5},
                        {"timestamp": 1716704557, "value": 0.7},
                        {"timestamp": 1716704547, "value": 0.4},
                        {"timestamp": 1716704537, "value": 0.6}]
                }
            },
        ]
    }
    ```

### `post_event`

**post_event**: This function posts an event to the Datadog monitoring system, allowing users to track significant occurrences or milestones. It returns a dictionary containing confirmation of the posted event.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | event_title | str | Title of the event | yes |
    | event_text | str | Detailed description of the event | yes |
    | event_tags | list | List of tags associated with the event | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains confirmation of the posted event, including its ID and timestamp |

=== "JSON"

    ```json
    {
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integration": "datadog",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "datadog/secret"
        },
        "action": [
            {   "post_event":{
                "event_title":"skyler_test_event",
                "event_text": "Testing event related stuff",
                "event_tags": ["test:ExampleEvent"]
            }},
        ]
    }
    ```

### `create_monitor`

**create_monitor**: This function creates a new monitor in Datadog to alert on specific conditions based on metric queries. It returns a dictionary containing details of the newly created monitor.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | monitor_name | str | Name of the monitor to be created | yes |
    | type | str | Type of the monitor (e.g., "query alert") | yes |
    | query | str | The metric query to evaluate for the monitor | yes |
    | message | str | Alert message to be sent when the monitor triggers | yes |
    | tags | list | List of tags associated with the monitor | yes |
    | priority | int | Priority level of the monitor | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains details of the newly created monitor, including its ID and status |

=== "JSON"

    ```json
        {
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integration": "datadog",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "datadog/secret"
        },
        "action": [
            {"create_monitor":
            {"monitor_name":"Skyler Test Monitor",
            "type": "query alert",
            "query": "avg(last_5m):avg:skyler.test{*} > 8",
            "message": "some message",
            "tags": ["test:skyler", "env:ci"],
            "priority": 3
            }}
        ]
    }
    ```

## Frequently Asked Questions

### What Datadog operations does EasyTask support?

EasyTask supports three primary Datadog operations: **submit_metrics** for sending time-series data points, **post_event** for recording significant occurrences or milestones, and **create_monitor** for setting up alert conditions based on metric queries. Each operation is invoked as an action within your scheduled task configuration.

### How do I submit custom metrics from scheduled tasks?

Use the `submit_metrics` action in your task payload. Provide the `metric_name`, `metric_intake_type` (e.g., 0 for gauge), a list of `tags`, and a list of `points` (each with a `timestamp` and `value`). EasyTask will submit these metric points to Datadog automatically when the scheduled task runs.

### Can I create Datadog monitors automatically?

Yes. Use the `create_monitor` action with the required parameters — `monitor_name`, `type`, `query`, `message`, `tags`, and `priority`. EasyTask will create the monitor in Datadog as part of your scheduled workflow, enabling hands-free alert setup and management.

## Next Steps

- [Integrations Overview](integrations_intro.md) — explore all available integrations.
- [Elasticsearch Integration](elastic_search.md) — index and search log data from scheduled tasks.
- [Slack Integration](slack.md) — send alerts and notifications to Slack channels.
