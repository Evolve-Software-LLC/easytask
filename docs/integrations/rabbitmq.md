---
description: "RabbitMQ integration for message queue management in automated workflows. Connect RabbitMQ to EasyTask for reliable message publishing, exchange and queue management, and message-driven task scheduling."
keywords:
  - RabbitMQ task scheduling
  - RabbitMQ message broker
  - queue automation
  - RabbitMQ integration EasyTask
  - message-driven workflows
  - exchange queue management
---

# RabbitMQ API

The RabbitMQ API provides a set of endpoints for managing exchanges, queues, and performing message operations. It allows users to interact with RabbitMQ clusters programmatically.

## Why Integrate RabbitMQ with EasyTask?

RabbitMQ is one of the most widely adopted open-source message brokers, trusted by enterprises for its reliability, flexibility, and support for multiple messaging protocols. By integrating RabbitMQ with EasyTask, you can publish messages to exchanges and queues on a schedule, manage exchanges and queues programmatically, and build reliable message-driven workflows without writing custom glue code. This integration is ideal for use cases such as order processing pipelines, notification delivery systems, event-driven microservices orchestration, and any scenario where tasks need to be triggered by or produce messages in a robust, decoupled manner.

## Required Values in Vault

```
{
"secret": {
   "password": "xxxxxxx",
   "rabbitmq_host": "xxx.xxx.xxx.xxx",
   "rabbitmq_port": "xxxxx",
   "username": "xxxxxxx"
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
        "integration": "rabbitmq",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "rabbitmq/secret"
        },
        "action": [
            {
                "setup_exchange": {
                    "exchange_name": "test_case_topic_exchange",
                    "exchange_type": "topic"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
        {
    "integration": "rabbitmq",
    "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
    "init": {
            "vault_path_key": "rabbitmq/server1"
    },
    "error":false
    "action": [
        {"setup_exchange":"test_case_topic_exchange is setup of type topic"}
    ]
        }
    ```

## Functions

### `setup_exchange`

**setup_exchange**: This function creates a new exchange in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | exchange_name | str | Name of the exchange to be created | yes |
    | exchange_type | str | Type of the exchange (e.g., "topic", "direct", "fanout") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the exchange is created successfully |

=== "JSON"

    ```json
    {
        "setup_exchange": {
            "exchange_name": "test_case_topic_exchange",
            "exchange_type": "topic"
        }
    }
    ```

### `setup_queue`

**setup_queue**: This function creates a new queue in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue to be created | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the queue is created successfully |

=== "JSON"

    ```json
    {
        "setup_queue": {
            "queue_name": "test_case_queue"
        }
    }
    ```

### `bind_queue`

**bind_queue**: This function binds a queue to an exchange in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | exchange_name | str | Name of the exchange | yes |
    | queue_name | str | Name of the queue to be bound | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the queue is bound successfully |

=== "JSON"

    ```json
    {
        "bind_queue": {
            "exchange_name": "test_case_topic_exchange",
            "queue_name": "test_case_queue"
        }
    }
    ```

### `bind_queues`

**bind_queues**: This function binds multiple queues to an exchange in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | exchange_name | str | Name of the exchange | yes |
    | queue_names | list | List of queue names to be bound | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if all queues are bound successfully |

=== "JSON"

    ```json
    {
        "bind_queues": {
            "exchange_name": "test_case_topic_exchange",
            "queue_names": ["test_case_queue1", "test_case_queue2", "test_case_queue3", "test_case_queue4"]
        }
    }
    ```

### `publish_message`

**publish_message**: This function publishes a message to a specific exchange and routing key in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | exchange | str | Name of the exchange to publish to | yes |
    | routing_key | str | Routing key for the message | yes |
    | message | str | Message content to be published | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the message is published successfully |

=== "JSON"

    ```json
    {
        "publish_message": {
            "exchange": "test_case_topic_exchange",
            "routing_key": "test_case_queue",
            "message": "My message"
        }
    }
    ```

### `get_message_from_queue`

**get_message_from_queue**: This function retrieves a message from a specific queue in RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue | str | Name of the queue to get the message from | yes |
    | callbackfn | str | Name of the callback function to handle the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains the message content and metadata |

=== "JSON"

    ```json
    {
        "get_message_from_queue": {
            "queue": "test_case_queue",
            "callbackfn": "callback2"
        }
    }
    ```

### `delete_queue`

**delete_queue**: This function deletes a queue from RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue to be deleted | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the queue is deleted successfully |

=== "JSON"

    ```json
    {
        "delete_queue": {
            "queue_name": "test_case_queue"
        }
    }
    ```

### `delete_exchange`

**delete_exchange**: This function deletes an exchange from RabbitMQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | exchange_name | str | Name of the exchange to be deleted | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the exchange is deleted successfully |

=== "JSON"

    ```json
    {
        "delete_exchange": {
            "exchange_name": "test_case_topic_exchange"
        }
    }
    ```

### `close_channel`

**close_channel**: This function closes the active channel in RabbitMQ.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the channel is closed successfully |

=== "JSON"

    ```json
    {
        "close_channel": {}
    }
    ```

### `close_connection`

**close_connection**: This function closes the active connection to RabbitMQ.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the connection is closed successfully |

=== "JSON"

    ```json
    {
        "close_connection": {}
    }
    ```

## Frequently Asked Questions

### What RabbitMQ operations does EasyTask support?

EasyTask supports a comprehensive set of RabbitMQ operations including creating and deleting exchanges (`setup_exchange`, `delete_exchange`), creating and deleting queues (`setup_queue`, `delete_queue`), binding queues to exchanges (`bind_queue`, `bind_queues`), publishing messages (`publish_message`), retrieving messages from queues (`get_message_from_queue`), and managing connections (`close_channel`, `close_connection`). Each operation can be used as an action step within your automated workflows.

### How do I publish messages in scheduled workflows?

You can publish messages by including the `publish_message` action in your workflow definition. Specify the target exchange, a routing key, and the message content as input parameters. When the workflow runs on its schedule, EasyTask connects to your RabbitMQ instance using credentials stored in the Vault and publishes the message automatically. See the [publish_message](#publish_message) function for the exact JSON structure.

### Can I manage exchanges and queues through EasyTask?

Yes. EasyTask provides dedicated functions for full lifecycle management of exchanges and queues. You can create exchanges of different types (topic, direct, fanout) using `setup_exchange`, create queues with `setup_queue`, bind one or more queues to an exchange with `bind_queue` or `bind_queues`, and clean up resources with `delete_exchange` and `delete_queue`. All of these operations are available as action steps in your scheduled workflows.

## Next Steps

- [Integrations Overview](integrations_intro.md) -- Explore all available integrations in EasyTask.
- [Kafka Integration](kafka.md) -- Learn how to connect EasyTask with Apache Kafka for distributed streaming.
- [Redis Integration](redis.md) -- Use EasyTask with Redis for caching, pub/sub, and data store operations.
