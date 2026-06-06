---
title: Discord - EasyTask Integration Guide
description: Connect Discord with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing webhooks and messages.
keywords:
  - discord
  - easytask
  - workflow orchestration
  - automation
  - messaging
  - webhooks
---

# Discord API

The Discord API provides a set of operations for interacting with Discord webhooks and messages, allowing users to send, edit, pin, and delete messages.

## Why Integrate Discord with EasyTask?

Integrating Discord with EasyTask enables you to automate messaging and notification workflows across your team channels. This integration allows you to:

- **Automate Notifications**: Send, edit, and manage Discord messages automatically as part of your EasyTask workflows, keeping your team informed in real time.
- **Manage Webhooks Programmatically**: Create, configure, and update Discord webhooks through EasyTask orchestration without manual intervention.
- **Streamline Channel Operations**: Pin important messages, retrieve message history, and clean up channels automatically as part of your automated processes.

## Required Values in Vault

```
"secret": {
    "channel_id": "xxxxxxxx",
    "token": "xxxxxxxx"
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
        "integration": "discord",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "discord/secret"
        },
        "action": [
            {
                "use_webhook": {
                    "webhook_url": "https://discord.com/api/webhooks/123456789/abcdefghijklmnop"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "discord",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "discord/secret"
        },
        "error": false,
        "action": [
            {"use_webhook": null}
        ]
    }

    ```

## Functions

### `use_webhook`

**use_webhook**: This function sets the webhook URL for subsequent operations.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | webhook_url | str | Discord webhook URL | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the webhook URL was set successfully |

=== "JSON"

    ```json
    {
        "use_webhook": {
            "webhook_url": "https://discord.com/api/webhooks/123456789/abcdefghijklmnop"
        }
    }
    ```

### `get_webhook_info`

**get_webhook_info**: This function retrieves information about the current webhook.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing webhook information |

=== "JSON"

    ```json
    {
        "get_webhook_info": {}
    }
    ```

### `get_all_webhooks`

**get_all_webhooks**: This function retrieves information about all webhooks in the channel.

=== "Input Parameters"

    This function takes no input parameters.

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing webhook information |

=== "JSON"

    ```json
    {
        "get_all_webhooks": {}
    }
    ```

### `update_webhook`

**update_webhook**: This function updates the name of the current webhook.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | webhook_name | str | New name for the webhook | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing updated webhook information |

=== "JSON"

    ```json
    {
        "update_webhook": {
            "webhook_name": "MyTestEvolveWebhook_Updated"
        }
    }
    ```

### `send_message`

**send_message**: This function sends a message to the Discord channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message | str | Message content to send | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | ID of the sent message |

=== "JSON"

    ```json
    {
        "send_message": {
            "message": "Hello, Discord!"
        }
    }
    ```

### `get_message`

**get_message**: This function retrieves a specific message by its ID.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message_id | str | ID of the message to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing message information |

=== "JSON"

    ```json
    {
        "get_message": {
            "message_id": "123456789"
        }
    }
    ```

### `edit_message`

**edit_message**: This function edits an existing message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message_id | str | ID of the message to edit | yes |
    | new_message | str | New content for the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing updated message information |

=== "JSON"

    ```json
    {
        "edit_message": {
            "message_id": "123456789",
            "new_message": "Updated message!"
        }
    }
    ```

### `pin_message`

**pin_message**: This function pins a message in the channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message_id | str | ID of the message to pin | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was pinned successfully |

=== "JSON"

    ```json
    {
        "pin_message": {
            "message_id": "123456789"
        }
    }
    ```

### `get_pinned_messages`

**get_pinned_messages**: This function retrieves all pinned messages in the channel.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing pinned message information |

=== "JSON"

    ```json
    {
        "get_pinned_messages": {}
    }
    ```

### `unpin_message`

**unpin_message**: This function unpins a message from the channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message_id | str | ID of the message to unpin | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was unpinned successfully |

=== "JSON"

    ```json
    {
        "unpin_message": {
            "message_id": "123456789"
        }
    }
    ```

### `delete_message`

**delete_message**: This function deletes a message from the channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message_id | str | ID of the message to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was deleted successfully |

=== "JSON"

    ```json
    {
        "delete_message": {
            "message_id": "123456789"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Discord credentials in EasyTask?
Use the EasyTask vault system to securely store your Discord bot token and channel ID. Navigate to the integration configuration page and add your credentials under a vault key like `discord/secret`.

### Can I use Discord with both EasyTask Cloud and On-Premises?
Yes, Discord works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical since Discord is a cloud-based service.

### How do I troubleshoot Discord connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your bot token and channel ID in the vault, ensure the Discord API is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
