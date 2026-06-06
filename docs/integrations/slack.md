---
title: Slack Integration - EasyTask Documentation
description: Slack integration for EasyTask — automate messaging, channel management, and notifications in your scheduled workflows.
keywords:
  - slack automation
  - easytask
  - scheduled messages
  - notification workflows
  - slack api
---

# Slack

Slack is a collaboration and messaging platform designed for teams to communicate efficiently. It allows real-time messaging, file sharing, and integration with various tools, streamlining workflows and enhancing productivity.

## Why Integrate Slack with EasyTask?

Slack is a leading business communication platform used by teams worldwide to collaborate in real time. By integrating Slack with EasyTask, your scheduled tasks can automatically send messages to channels or individuals, manage conversations, and automate notification workflows — all without manual intervention. This integration is ideal for incident alerting, automated report delivery, real-time status updates, and keeping your team informed through every step of a scheduled pipeline.

## Integration Server Vault details

### Required Secret in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "slack_bot_token": ".........",
        "slack_user_token": "........"
      }
    }
    ```

### Get BOT & USER Token

The following steps tell you how to generate the bot and user token:

1. First, you need to register yourself in Slack API.
2. After registering, create an app in Slack.
3. After creating, on the left side of the page, you can see the OAuth & Permissions section. Select that, and you can see OAuth Tokens for Your Workspace. Below that, there will be User OAuth Token and Bot User OAuth Token. Click on generate, and a unique token will be generated for you.
4. Store that token in an .env file so that all credentials are safe.

### Slack Integration JSON Format

An SlackIntegration can be created as below by passing the vault_path_key:

=== "Input"

    ```json
    [
      {
        "user": "test user",
        "integration": "slack",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "slack/server1"
        },
        "action": []
      }
    ]
    ```

=== "Output"

    ```json
    [
      {
        "integration": "slack",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "slack/server1"
        },
        "error": false,
        "action": []
      }
    ]
    ```

## Example cURL Commands

### Sample Usage of Slack 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d
      '[
        {
            "user": "test user",
            "integration": "slack",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "slack/server1"
            },
            "action": [
                {
                    "send_private_message": {
                        "channel": "#rest-api",
                        "message": "Hello There",
                        "user_id": "U03BBNM8FM5"
                    }
                }
            ]
        }
      ]'
    ```

=== "Output"

    ```json
    {
        {
           "send_private_message": null
        }
    }
    ```

## Functions

### `get_basic_info`

This function retrieves basic information like username, team_id, user_id, bot_id, etc.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "get_basic_info": {}
            }
          ]
        }
      ]
    }
    ```

### `send_private_message`

This function sends a private message to a particular user present in an existing channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | message | string | Message to be sent | Yes |
    | user_id | string | User ID of the recipient | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "send_private_message": {
                "channel": "#rest-api",
                "message": "Hello There",
                "user_id": "U03BBNM8FM5"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_message`

This function sends a normal message to a channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | message | string | Message to be sent | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "send_message": {
                "channel": "#rest-api",
                "message": "hello from json"
              }
            }
          ]
        }
      ]
    }
    ```

### `find_conversation_id`

This function retrieves the conversation id of a given channel name.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "find_conversation_id": {
                "channel": "rest-api"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_channel_id`

This function fetches the channel id to perform updating and deleting of messages. It returns all the ids of channels along with the channel names present in Slack in dictionary format.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "get_channel_id": {}
            }
          ]
        }
      ]
    }
    ```

### `retreive_message`

This function retrieves all messages from a particular channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "retreive_message": {
                "channel": "rest-api"
              }
            }
          ]
        }
      ]
    }
    ```

### `modify_message`

This function updates a message in the channel by passing channel_id, timestamp of the message, and the message to be updated.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | timestamp | string | Timestamp of the message | Yes |
    | text | string | New message content | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "modify_message": {
                "channel": "rest-api",
                "timestamp": "<TIMESTAMP OF THE MESSAGE>",
                "text": "<YOUR MESSAGE>"
              }
            }
          ]
        }
      ]
    }
    ```

Note: You can get the timestamp of the message by calling the `retreive_message()` method. Timestamp is a string, for example: `ts = "1710317688.175729"`.

### `delete_message`

This function deletes a message in the channel by providing channel_id and timestamp.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | timestamp | string | Timestamp of the message | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "slack",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "slack/server1"
          },
          "action": [
            {
              "delete_message": {
                "channel": "rest-api",
                "timestamp": "<TIMESTAMP OF THE MESSAGE>"
              }
            }
          ]
        }
      ]
    }
    ```

## Frequently Asked Questions

### What Slack operations does EasyTask support?

EasyTask supports a range of Slack operations including `send_message`, `send_private_message`, `retreive_message`, `modify_message`, `delete_message`, `find_conversation_id`, `get_channel_id`, and `get_basic_info`. These actions cover common messaging and channel management tasks that can be embedded into any scheduled workflow.

### How do I send automated Slack notifications from scheduled tasks?

Create a scheduled task in EasyTask and use the Slack integration by providing your `vault_path_key` containing the Slack bot and user tokens. Then add a `send_message` or `send_private_message` action with the target channel and message content. When the schedule triggers, EasyTask will automatically post the notification to the specified Slack channel or user.

### Can I modify and delete Slack messages through EasyTask?

Yes. Use the `modify_message` action to update an existing message by providing the channel name, message timestamp, and new text. Use the `delete_message` action to remove a message by providing the channel name and timestamp. You can obtain message timestamps by first calling the `retreive_message` action.

## Next Steps

- [Integrations Overview](integrations_intro.md)
- [Microsoft Teams Integration](msteams.md)
- [Datadog Integration](datadogs.md)
