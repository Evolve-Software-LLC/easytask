---
title: NSQ Message Queue - EasyTask Integration Guide
description: Connect NSQ with EasyTask for automated message queue operations. Step-by-step setup, configuration, and best practices for NSQMQ integration.
keywords:
  - nsq
  - nsqmq
  - message queue
  - easytask
  - workflow orchestration
  - automation
---

# NSQMQ API

The NSQMQ API provides a set of operations for interacting with NSQ (Next-Generation Message Queue), allowing users to manage topics, channels, publish messages, and consume data.

## Why Integrate NSQ with EasyTask?

Integrating NSQ with EasyTask enables you to automate message queue management and event-driven workflows. This integration allows you to:

- **Automate Topic and Channel Management**: Programmatically create, pause, unpause, and delete topics and channels as part of your deployment and scaling workflows.
- **Streamline Message Publishing and Consumption**: Publish and consume messages in bulk with automated retry and error handling built into your EasyTask pipelines.
- **Centralize NSQ Configuration**: Store NSQ daemon addresses and ports securely in the EasyTask vault for consistent, environment-aware connections.

## Required Values in Vault

```
{
   "secret": {
         "host": "xxxxxxxx (String Type)",
         "nsqd_http_port": "xxxxxxxx (Int Type)",
         "nsqd_tcp_port": "xxxxxxxx (Int Type)",
         "nsqdlookupd_http_port": "xxxxxxxx (Int Type)"
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
        "integration": "nsqmq",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "nsqmq/secret"
        },
        "action": [
            {
                "create_topic": {
                    "topic": "json_test_topic"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "nsq",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
        "vault_path_key": "nsq/server1"
        },
        "error": false,
        "action": [
            {
                "create_topic": null
            }
        ]
    }

    ```

## Functions

### `create_topic`

**create_topic**: This function creates a new topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the topic was created successfully |

=== "JSON"

    ```json
    {
        "create_topic": {
            "topic": "json_test_topic"
        }
    }
    ```

### `create_channel`

**create_channel**: This function creates a new channel for a specific topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |
    | channel | str | Name of the channel to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the channel was created successfully |

=== "JSON"

    ```json
    {
        "create_channel": {
            "topic": "json_test_topic",
            "channel": "json_test_channel"
        }
    }
    ```

### `empty_topic`

**empty_topic**: This function empties all messages from a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to empty | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the topic was emptied successfully |

=== "JSON"

    ```json
    {
        "empty_topic": {
            "topic": "json_test_topic"
        }
    }
    ```

### `empty_channel`

**empty_channel**: This function empties all messages from a specific channel of a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |
    | channel | str | Name of the channel to empty | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the channel was emptied successfully |

=== "JSON"

    ```json
    {
        "empty_channel": {
            "topic": "json_test_topic",
            "channel": "json_test_channel"
        }
    }
    ```

### `pause_topic`

**pause_topic**: This function pauses message flow for a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to pause | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the topic was paused successfully |

=== "JSON"

    ```json
    {
        "pause_topic": {
            "topic": "json_test_topic"
        }
    }
    ```

### `unpause_topic`

**unpause_topic**: This function resumes message flow for a paused topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to unpause | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the topic was unpaused successfully |

=== "JSON"

    ```json
    {
        "unpause_topic": {
            "topic": "json_test_topic"
        }
    }
    ```

### `pause_channel`

**pause_channel**: This function pauses message flow for a specific channel of a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |
    | channel | str | Name of the channel to pause | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the channel was paused successfully |

=== "JSON"

    ```json
    {
        "pause_channel": {
            "topic": "json_test_topic",
            "channel": "json_test_channel"
        }
    }
    ```

### `unpause_channel`

**unpause_channel**: This function resumes message flow for a paused channel of a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |
    | channel | str | Name of the channel to unpause | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the channel was unpaused successfully |

=== "JSON"

    ```json
    {
        "unpause_channel": {
            "topic": "json_test_topic",
            "channel": "json_test_channel"
        }
    }
    ```

### `get_all_topics`

**get_all_topics**: This function retrieves a list of all topics in NSQ.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all topic names |

=== "JSON"

    ```json
    {
        "get_all_topics": {}
    }
    ```

### `get_all_channels`

**get_all_channels**: This function retrieves a list of all channels for a specific topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all channel names for the specified topic |

=== "JSON"

    ```json
    {
        "get_all_channels": {
            "topic": "json_test_topic"
        }
    }
    ```

### `publish`

**publish**: This function publishes one or more messages to a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to publish to | yes |
    | message | list | List of messages to publish | yes |
    | mpub | bool | If true, publish multiple messages in a single request | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the messages were published successfully |

=== "JSON"

    ```json
    {
        "publish": {
            "topic": "json_test_topic",
            "message": ["json message", "hello world"],
            "mpub": true
        }
    }
    ```

### `consume`

**consume**: This function consumes messages from a specific channel of a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to consume from | yes |
    | channel | str | Name of the channel to consume from | yes |
    | block | bool | If true, block until messages are available | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of consumed messages |

=== "JSON"

    ```json
    {
        "consume": {
            "topic": "json_test_topic",
            "channel": "json_test_channel",
            "block": false
        }
    }
    ```

### `delete_channel`

**delete_channel**: This function deletes a channel from a topic in NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic | yes |
    | channel | str | Name of the channel to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the channel was deleted successfully |

=== "JSON"

    ```json
    {
        "delete_channel": {
            "topic": "json_test_topic",
            "channel": "json_test_channel"
        }
    }
    ```

### `delete_topic`

**delete_topic**: This function deletes a topic from NSQ.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | topic | str | Name of the topic to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the topic was deleted successfully |

=== "JSON"

    ```json
    {
        "delete_topic": {
            "topic": "json_test_topic"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure NSQ credentials in EasyTask?
Use the EasyTask vault system to securely store your NSQ connection details. Navigate to the integration configuration page and add your server details under a vault key like `nsq/server1`. Include the host, nsqd HTTP port, nsqd TCP port, and nsqlookupd HTTP port.

### Can I use NSQ with both EasyTask Cloud and On-Premises?
Yes, NSQ works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the NSQ daemons are reachable from the integration server.

### How do I troubleshoot NSQ connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your host and port settings in the vault, ensure the NSQ daemons (nsqd and nsqlookupd) are accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
