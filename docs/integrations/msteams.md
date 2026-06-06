---
description: "Microsoft Teams integration for EasyTask — automate adaptive card messaging and notifications in enterprise workflows. Send rich messages, interactive actions, and status broadcasts directly to MS Teams channels."
keywords:
  - MS Teams automation
  - adaptive cards
  - enterprise notifications
  - Microsoft Teams integration
  - Teams webhook
  - EasyTask MS Teams
  - scheduled Teams messages
  - approval workflows Teams
---

# Microsoft Teams API

The Microsoft Teams API provides a set of operations for creating and sending rich messages to Microsoft Teams channels.

## Why Integrate Microsoft Teams with EasyTask?

Microsoft Teams is the central hub for enterprise communication and collaboration, used by millions of organizations worldwide to coordinate work, share updates, and drive decisions. By integrating MS Teams with EasyTask, you unlock the ability to have scheduled tasks automatically send rich adaptive card messages — complete with links, interactive actions, and themed formatting — directly to the Teams channels your teams already monitor.

This integration is ideal for powering **executive dashboards** with real-time KPI summaries, building **approval workflows** where stakeholders can respond inline without leaving Teams, and delivering **enterprise-wide status broadcasts** that keep everyone aligned. Instead of manually posting updates or relying on developers to build custom bots, EasyTask lets you configure and automate these messages through simple task definitions — saving time and ensuring consistency across your organization.

## Required Values in Vault

```
{
   "secret": {
      "webhook_url": "https://aitpuneedu.webhook.office.com/webhookb2/............"
   }
}
```

## Integration Server Vault details

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
        "integration": "msteams",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "msteams/secret"
        },
        "action": [
            {
                "add_title": {
                    "title": "test_table_new"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {

        "integration": "msteams",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "msteams/server1"
        },
        "error": false,
        "action": [
            {
                "add_title": "Title added successfully"
            }
        ]
    }

    ```

## Functions

### `add_title`

**add_title**: This function adds a title to the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | title | str | Title of the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the title was added successfully |

=== "JSON"

    ```json
    {
        "add_title": {
            "title": "test_table_new"
        }
    }
    ```

### `add_text`

**add_text**: This function adds text content to the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | text | str | Text content of the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the text was added successfully |

=== "JSON"

    ```json
    {
        "add_text": {
            "text": "test_table_new"
        }
    }
    ```

### `add_link_buttons`

**add_link_buttons**: This function adds link buttons to the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buttons | dict | Dictionary of button labels and URLs | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the buttons were added successfully |

=== "JSON"

    ```json
    {
        "add_link_buttons": {
            "buttons": {
                "Pypi": "https://pypi.org/",
                "PEP-8": "https://pep8.org"
            }
        }
    }
    ```

### `set_color_theme`

**set_color_theme**: This function sets the color theme of the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | theme | str | Color theme for the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the color theme was set successfully |

=== "JSON"

    ```json
    {
        "set_color_theme": {
            "theme": "red"
        }
    }
    ```

### `preview`

**preview**: This function generates a preview of the Teams message.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Preview of the message |

=== "JSON"

    ```json
    {
        "preview": {}
    }
    ```

### `add_actions`

**add_actions**: This function adds interactive actions to the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | actions_dict | list | List of action dictionaries | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the actions were added successfully |

=== "JSON"

    ```json
    {
        "add_actions": {
            "actions_dict": [
                {
                    "actions": [{
                        "name": "Save Status",
                        "target": "https://docs.microsoft.com/outlook/actionable-messages",
                        "type": "HttpPost"
                    }],
                    "inputs": [{
                        "choices": [
                            {
                                "display": "In Progress",
                                "value": "1"
                            },
                            {
                                "display": "Activate",
                                "value": "2"
                            },
                            {
                                "display": "Closed",
                                "value": "3"
                            }
                        ],
                        "id": "list",
                        "title": "Pick one",
                        "type": "MultichoiceInput"
                    }],
                    "name": "Status"
                },
                {
                    "actions": [{
                        "name": "Save Date",
                        "target": "https://docs.microsoft.com/outlook/actionable-messages",
                        "type": "HttpPost"
                    }],
                    "inputs": [{
                        "id": "dueDate",
                        "title": "Pick due date",
                        "type": "DateInput"
                    }],
                    "name": "Due Date"
                },
                {
                    "actions": [{
                        "name": "Post",
                        "target": "https://docs.microsoft.com/outlook/actionable-messages",
                        "type": "HttpPost"
                    }],
                    "inputs": [{
                        "id": "comment",
                        "title": "Comment ...",
                        "type": "TextInput"
                    }],
                    "name": "Comment"
                }
            ]
        }
    }
    ```

### `add_sections`

**add_sections**: This function adds sections to the Teams message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | sections_dict | list | List of section dictionaries | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the sections were added successfully |

=== "JSON"

    ```json
    {
        "add_sections": {
            "sections_dict": [
                {
                    "title": "Python",
                    "text": "Python is a programming language that lets you work quickly and integrate systems more effectively",
                    "images": [{
                        "url": "https://www.python.org/static/img/python-logo.png",
                        "alt": "python logo"
                    }],
                    "facts": [{
                        "name": "3.10",
                        "value": "2021-10-04"
                    }, {
                        "name": "3.9",
                        "value": "2021-10-05"
                    }],
                    "activities": [{
                        "title": "PyCon Kenya Conference 2022",
                        "subtitle": "2022-05-06",
                        "image": "https://www.python.org/static/img/python-logo.png",
                        "text": "Python Conference in Kenya"
                    }]  
                }
            ]
        }
    }
    ```

### `send_message`

**send_message**: This function sends the constructed message to Microsoft Teams.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was sent successfully |

=== "JSON"

    ```json
    {
        "send_message": {}
    }
    ```

### `construct_and_send_msg`

**construct_and_send_msg**: This function constructs and sends a message to Microsoft Teams in a single operation.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the message was constructed and sent successfully |

=== "JSON"

    ```json
    {
        "construct_and_send_msg": {}
    }
    ```

## FAQ

### What Microsoft Teams operations does EasyTask support?

EasyTask supports a comprehensive set of MS Teams operations including `add_title`, `add_text`, `add_link_buttons`, `set_color_theme`, `add_actions`, `add_sections`, `preview`, `send_message`, and `construct_and_send_msg`. These operations allow you to build rich adaptive card messages step by step and send them to any Teams channel via an incoming webhook.

### How do I send an adaptive card message to a Teams channel?

First, store your Teams incoming webhook URL in the EasyTask vault. Then, in your task definition, use the `msteams` integration and chain actions such as `add_title`, `add_text`, `add_sections`, and `add_actions` to build the adaptive card. Finally, call `send_message` (or `construct_and_send_msg` for a one-shot operation) to deliver the message to your channel.

### Can I customize message themes and interactive actions?

Yes. Use the `set_color_theme` function to apply a color theme (e.g., red, green, blue) to your adaptive card. You can add interactive elements with `add_actions`, which supports input types like `MultichoiceInput`, `DateInput`, and `TextInput`, as well as `HttpPost` action buttons — perfect for approval workflows and status updates.

## Next Steps

- [Integrations Overview](integrations_intro.md) — explore all available EasyTask integrations
- [Slack Integration](slack.md) — send automated messages to Slack workspaces
- [Jira Integration](jira.md) — automate issue tracking and project management tasks
