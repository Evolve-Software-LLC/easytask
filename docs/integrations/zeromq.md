---
title: ZeroMQ - EasyTask Integration Guide
description: Connect ZeroMQ with EasyTask for automated messaging, queue management, and pub/sub communication in scheduled workflows.
keywords:
  - zeromq
  - easytask
  - workflow orchestration
  - automation
  - messaging
  - message queue
  - zeromq integration
---

# ZeroMQ

ZeroMQ is a library used to implement messaging and communication systems between applications and processes - fast and asynchronously.

## Why Integrate ZeroMQ with EasyTask?

ZeroMQ is a high-performance asynchronous messaging library used for building distributed and concurrent applications. By integrating ZeroMQ with EasyTask, you can automate message queue management, pub/sub communication, and inter-process messaging on a configurable schedule. EasyTask enables you to send and receive messages, manage topics and queues, and orchestrate message-driven workflows — all triggered by scheduled tasks. This integration is ideal for building automated data pipelines, scheduling message distribution, and managing microservice communication without manual intervention.

## Integration Server Vault details

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "host": "xx.x.xx.xxx",
        "port": "xxxx"
      }
    }
    ```

=== "Table"

    | Key | Type | Description |
    |-----|------|-------------|
    | host | string | The hostname or IP address of the server |
    | port | string | The port number for the connection |

## Example cURL Commands

### Sample Usage of ZeroMQ 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d
      '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
              "vault_path_key":"zmq/secret"
          },
          "action": [
              {"add_to_queue":{
                  "message":"message"
          }
            }
          ]
        ]

      }'
    ```

=== "Output"

    ```json
    {
        {
          "add_to_queue": "Added to queue"
        }
    }
    ```

## Functions

### ZeroMQ Integration JSON Format

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": []
        }
      ]
    }
    ```

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | init.vault_path_key | string | Path to the vault containing ZeroMQ credentials |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions to be performed (empty in this example) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": []
        }
      ]
    }
    ```

### `add_to_queue`

**Add to Queue**:

This function adds data to the queue to be sent.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | message | string | Message to be added | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the add_to_queue action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": [
            {
              "add_to_queue": {
                "message": "message"
              }
            }
          ]
        }
      ]
    }
    ```

### `connect_to_server`

**Connect to Server**:

This function connects to the server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | client_id | string | Client id | Yes |
    | queue_name | string | Name of queue client wants to send data to | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the connect_to_server action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": [
            {
              "connect_to_server": {
                "client_id": "jayant",
                "queue_name": "big_message"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_queue`

**Send Queue**:

This function sends the entire queue at once.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | messages | array[string] | Array of messages to be sent | Yes |
    | client_id | string | Client id | Yes |
    | queue_name | string | Name of the queue client wants to send data to | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the send_queue action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": [
            {
              "send_queue": {
                "messages": ["hello world", "Goodbye world"],
                "client_id": "jayant",
                "queue_name": "big_message"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_quick_message`

**Send Quick Message**:

This function sends a single message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | message | string | Message to be sent | Yes |
    | client_id | string | Client id | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the send_quick_message action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": [
            {
              "send_quick_message": {
                "message": "hello there",
                "client_id": "Client 2"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_messages_from_topic`

**Get Messages from Topic**:

This function gets messages from server on a particular topic.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | topic | string | Particular topic | Yes |
    | port | string | Port number to connect to | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zeromq) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_messages_from_topic action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zeromq",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zmq/secret"
          },
          "action": [
            {
              "get_messages_from_topic": {
                "topic": "test2"
              }
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What ZeroMQ operations does EasyTask support?

EasyTask supports core ZeroMQ messaging operations including adding messages to queues, retrieving messages from topics, and managing pub/sub communication patterns. You can automate message distribution and consumption through scheduled tasks.

### How do I configure ZeroMQ connections in EasyTask?

Store your ZeroMQ connection details (host and port) in the EasyTask vault using a path key like `zmq/secret`. Reference this vault path key in your integration configuration to establish secure messaging channels without exposing connection details in task definitions.

### Can I use ZeroMQ for inter-service communication in automated workflows?

Yes. ZeroMQ's lightweight messaging patterns (pub/sub, push/pull, request/reply) make it ideal for building automated inter-service communication workflows. Combined with EasyTask scheduling, you can automate message routing between microservices, schedule data distribution, and manage event-driven pipelines.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
