---
title: Solace - EasyTask Integration Guide
description: Connect Solace PubSub+ with EasyTask for automated event streaming, message management, and real-time data orchestration in scheduled workflows.
keywords:
  - solace
  - easytask
  - workflow orchestration
  - automation
  - event streaming
  - message queue
  - pubsub
---

# Solance

Solace PubSub+ is a complete event streaming and management platform for the real-time enterprise.

## Why Integrate Solace with EasyTask?

Solace PubSub+ provides enterprise-grade event streaming and real-time data distribution across hybrid and multi-cloud environments. By integrating Solace with EasyTask, you can automate message queue management, topic configuration, and event-driven workflows on a configurable schedule. EasyTask enables you to publish and subscribe to messages, manage queues and topics, monitor connections, and orchestrate complex event pipelines — all triggered by scheduled tasks. This integration is ideal for building real-time data processing workflows, automating IoT data ingestion, and managing event-driven microservice communication without manual intervention.

## Integration Server Vault details

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "SEMP_port": "xxxx",
        "host": "xx.x.xx.xxx",
        "password": "xxxxxxxx",
        "username": "xxxxxxxx",
        "vpn": "xxxxxxxx",
        "web_transport_port": "xxxx"
      }
    }
    ```

### Solace integration JSON Format

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "solace") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing Solace credentials | Yes |
    | action | array | List of actions to be performed (empty in this example) | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": []
        }
      ]
    }
    ```

=== "Output JSON"

    ```json
    [
      {
        "integration": "solace",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "solace/server1"
        },
        "error": false,
        "action": []
      }
    ]
    ```

## Example cURL Commands

### Sample Usage of Solance 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d' 
      {
        "is_credentials": {
          "userid": "test",
          "passwd": "test123"
        },
        "integrations": [
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
              "vault_path_key":"solace/server1"
          },
          "action": [
              {"add_queue": {
                  "queue_name":"test-queue1",
                  "vpn_name":"default"
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
          "add_queue": "Queue 'test-queue1' created successfully"
        }
    }
    ```

## Functions

### `add_queue`

**Add a Queue**:

This function adds a queue to the VPN.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | queue_name | string | Name of the queue | Yes |
    | vpn_name | string | Name of the VPN | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the add_queue action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "add_queue": {
                "queue_name": "test-queue1",
                "vpn_name": "default"
              }
            }
          ]
        }
      ]
    }
    ```

### `add_topic_queue`

**Add Topic Queue**:

This function adds a topic to the queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | queue_name | string | Name of the queue | Yes |
    | vpn_name | string | Name of the VPN | Yes |
    | topic_name | string | Name of the topic | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the add_topic_queue action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "add_topic_queue": {
                "queue_name": "test-queue1",
                "topic_name": "test-topic",
                "vpn_name": "default"
              }
            }
          ]
        }
      ]
    }
    ```

### `publish_direct_message`

**Publish direct message**:

This function publishes direct messages.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | topic_name | string | Topic to send the message | Yes |
    | message | string | Message to be sent | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the publish_direct_message action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "publish_direct_message": {
                "topic_name": "testss",
                "message": "Testing direct message"
              }
            }
          ]
        }
      ]
    }
    ```

### `publish_many_direct_messages`

**Publish many direct messages**:

This function publishes direct messages in bulk.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | data | array | List of dictionaries containing topic_name and message | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the publish_many_direct_messages action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "publish_many_direct_messages": {
                "data": [
                  {
                    "topic_name": "test11",
                    "message": "your_message"
                  },
                  {
                    "topic_name": "test12",
                    "message": "your_message"
                  },
                  {
                    "topic_name": "test15",
                    "message": "your_message"
                  }
                ]
              }
            }
          ]
        }
      ]
    }
    ```

### `publish_persistent_message`

**Publish persistent message**:

This function publishes a string message using persistent message publisher, non-blocking.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | topic_name | string | Topic to send the message | Yes |
    | message | string | Message to be sent | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the publish_persistent_message action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "publish_persistent_message": {
                "topic_name": "testss",
                "message": "Testing direct message"
              }
            }
          ]
        }
      ]
    }
    ```

### `publish_many_persistent_messages`

**Publish many persistent messages**:

This function publishes persistent messages in bulk.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | data | array | List of dictionaries containing topic_name and message | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the publish_many_persistent_messages action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "publish_many_persistent_messages": [
                {
                  "topic_name": "test-topic1",
                  "message": "your_message"
                },
                {
                  "topic_name": "test-topic2",
                  "message": "your_message"
                },
                {
                  "topic_name": "test-topic3",
                  "message": "your_message"
                }
              ]
            }
          ]
        }
      ]
    }
    ```

### `delete_queue`

**Delete Queue**:

This function deletes a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | queue_name | string | Name of the queue | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_queue action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "delete_queue": {
                "queue_name": "test-queue1"
              }
            }
          ]
        }
      ]
    }
    ```

### `disconnect`

**Disconnect**:

This function disconnects the messaging service.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (solace) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the disconnect action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "solace",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "solace/server1"
          },
          "action": [
            {
              "disconnect": {}
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What Solace operations does EasyTask support?

EasyTask supports a comprehensive set of Solace PubSub+ operations including connecting and disconnecting from message brokers, publishing and subscribing to messages, managing queues and topics, and monitoring connection status. You can automate the full lifecycle of event-driven messaging through scheduled tasks.

### How do I configure Solace credentials in EasyTask?

Store your Solace connection details (host, SEMP port, web transport port, VPN name, username, and password) in the EasyTask vault using a path key like `solace/server1`. Reference this vault path key in your integration configuration to securely authenticate without exposing credentials in task definitions.

### Can I automate real-time event processing with Solace?

Yes. By combining Solace's pub/sub capabilities with EasyTask's scheduling engine, you can create workflows that automatically process incoming events, transform data, and route messages to downstream systems. Schedule tasks to monitor queues, manage subscriptions, and handle message backpressure automatically.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
