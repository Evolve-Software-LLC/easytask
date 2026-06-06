---
description: Integrate Apache Kafka with EasyTask for topic listing and message production in scheduled workflows. Automate event-driven pipelines with Kafka scheduling and task automation.
keywords:
  - Kafka scheduling
  - task automation
  - message broker
  - Kafka integration
  - event streaming
  - EasyTask Kafka
---

# Kafka API

The Kafka API provides a set of operations for interacting with Apache Kafka, allowing users to manage topics and produce messages.

## Why Integrate Kafka with EasyTask?

Apache Kafka is the most widely used distributed event streaming platform, powering real-time data feeds and event-driven architectures at scale. By integrating Kafka with EasyTask, your scheduled tasks can produce messages to Kafka topics and build event-driven workflows that react to time-based triggers automatically.

This integration is especially valuable for:

- **Financial data pipelines** — reliably stream trade, transaction, and market data on schedule.
- **Real-time analytics** — push processed metrics and aggregated results to Kafka topics as part of recurring batch jobs.
- **Microservice orchestration** — use scheduled workflows to publish commands and events that other services consume, decoupling your system architecture.

## Required Values in Vault

```
{
   "secret": {
         "host": "xxxxxxxx (String Type)",
         "port": "xxxxxxxx (String Type)"
   }
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
        "integration": "kafka",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "kafka/secret"
        },
        "action": [
            {
                "list_topic": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
        
    {
        "integration": "kafka",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "kafka/server1"
        },
        "error": false,
        "action": [
            {
            "list_topic": {
                "test_topic": null,
                "test": null
            }
            }
        ]
    }

    ```

## Functions

### `list_topic`

**list_topic**: This function retrieves a list of all topics in the Kafka cluster.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of topic names in the Kafka cluster |

=== "JSON"

    ```json
    {
        "list_topic": {}
    }
    ```

### `produce_to_topic`

**produce_to_topic**: This function produces a message to a specified Kafka topic.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic_name | str | Name of the topic to produce to | yes |
    | message | str | Message to be produced | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was successfully produced, False otherwise |

=== "JSON"

    ```json
    {
        "produce_to_topic": {
            "topic_name": "test",
            "message": "hello"
        }
    }
    ```

## Frequently Asked Questions

### What Kafka operations does EasyTask support?

EasyTask currently supports two Kafka operations: **list_topic** (retrieve all topic names in the cluster) and **produce_to_topic** (publish a message to a specified topic). These operations can be used within any scheduled workflow.

### How do I produce messages to a Kafka topic in a scheduled workflow?

Use the `produce_to_topic` action in your workflow definition, providing the `topic_name` and `message` parameters. Store your Kafka broker credentials (host and port) in the EasyTask Vault, then reference the vault path in the `init` block of your request.

### Can I list Kafka topics from EasyTask?

Yes. Call the `list_topic` action with an empty object `{}`. It returns a list of all topic names available in the connected Kafka cluster, making it easy to verify topics before producing messages.

## Next Steps

- [Integrations Overview](integrations_intro.md) — explore all available integrations.
- [RabbitMQ Integration](rabbitmq.md) — compare with another popular message broker.
- [Redis Integration](redis.md) — use Redis for caching and pub/sub in your workflows.
