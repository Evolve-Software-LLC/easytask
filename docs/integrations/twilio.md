---
title: Twilio - EasyTask Integration Guide
description: Connect Twilio with EasyTask for automated SMS messaging, voice calls, and communication workflows in scheduled tasks.
keywords:
  - twilio
  - easytask
  - workflow orchestration
  - automation
  - sms
  - voice calls
  - messaging
  - twilio integration
---

# Twilio

Twilio is a messaging platform to send text messages and calls.

## Why Integrate Twilio with EasyTask?

Twilio is the leading cloud communications platform for SMS, voice, and messaging applications. By integrating Twilio with EasyTask, you can automate SMS notifications, voice calls, and communication workflows on a configurable schedule. EasyTask enables you to send text messages, initiate phone calls, retrieve call logs, and manage phone numbers — all triggered by scheduled tasks. This integration is ideal for building automated alerting systems, scheduling customer notifications, and orchestrating multi-channel communication workflows without manual intervention.

## Integration Server Vault details

### Required secret in Vault

=== "Table"

    | Key | Type | Description |
    |-----|------|-------------|
    | account_sid | string | Account SID for Twilio |
    | auth_token | string | Auth token for Twilio |
    | http_proxy | string | Proxy URL if you want to use a proxy |

=== "JSON"

    ```json
    {
      "secret": {
        "account_sid": "your account sid",
        "auth_token": "your account auth token",
        "http_proxy": "proxy if setup"
      }
    }
    ```

### Twilio Integration JSON Format

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "twilio") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing Twilio credentials | Yes |
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
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of Twilio 

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
        {
            "integrations": [
                {
                    "integration": "twilio",
                    "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                    "init": {
                        "vault_path_key": "twilio/server1"
                    },
                    "action": [
                        {"make_call":{
                            "call_to": "+91XXXXXXXXXX",
                            "call_from": "+1XXXXXXXXXX",
                            "twiml": "<Response><Say>Ahoy, World!</Say></Response>"
                        }}
                    ]
                }
            ]
        }

      }'
    ```

=== "Output"

    ```json
    {
        {
          "make_call": "CA8f5d1a4fb1d344115c7a5a4b728f79f6"
        }
    }
    ```

## Functions

### `make_call`

**Make a call**:

This function makes a single call to a given number and says a message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | call_to | string | The number you wish to call to | Yes |
    | call_from | string | The number you wish to call from | Yes |
    | twiml | string | TwiML instructions for the call Twilio will use | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the make_call action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "make_call": {
                "call_to": "+91XXXXXXXXXX",
                "call_from": "+1XXXXXXXXXX",
                "twiml": "<Response><Say>Ahoy, World!</Say></Response>"
              }
            }
          ]
        }
      ]
    }
    ```

### `make_call_async`

**Make multiple calls asynchronously**:

This function makes multiple calls to unique numbers with unique TwiML instructions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | data | array[array[string, string]] | Array of arrays containing call_to numbers and TwiML instructions | Yes |
    | call_from | string | The number you wish to call from | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the make_call_async action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "make_call_async": {
                "data": [
                  ["+91XXXXXXXXXX", "<Response><Say>Message 1</Say></Response>"],
                  ["+91XXXXXXXXXX", "<Response><Say>Message 2</Say></Response>"]
                ],
                "call_from": "+1XXXXXXXXXX"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_message`

**Send a single message**:

This function sends a single message to a specified number.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | message_to | string | The number you wish to message to | Yes |
    | message_from | string | The number you wish to message from | Yes |
    | body | string | The message body | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the send_message action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "send_message": {
                "message_to": "+91XXXXXXXXXX",
                "message_from": "+1XXXXXXXXXX",
                "body": "Ahoy, World!"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_messages_async`

**Send multiple messages asynchronously**:

This function sends multiple messages to unique numbers with unique message bodies.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | data | array[array[string, string]] | List containing lists with 2 string values: number to message and message body | Yes |
    | message_from | string | The number from which you wish to message | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the send_messages_async action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "send_messages_async": {
                "data": [
                  ["+91XXXXXXXXXX", "Message 1"],
                  ["+91XXXXXXXXXX", "Message 2"]
                ],
                "message_from": "+1XXXXXXXXXX"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_message_logs`

**Get message logs**:

This function retrieves logs for past messages.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | page_size | integer | Max number of logs to show in your request (defaults to 50) | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_message_logs action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "get_message_logs": {}
            }
          ]
        }
      ]
    }
    ```

### `get_call_logs`

**Get call logs**:

This function retrieves logs for past calls.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | page_size | integer | Max number of logs to show in your request (defaults to 50) | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (twilio) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_call_logs action |

=== "JSON"

    ```sh
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "twilio",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "twilio/server1"
          },
          "action": [
            {
              "get_call_logs": {}
            }
          ]
        }
      ]
}
    ```

## FAQ

### What Twilio operations does EasyTask support?

EasyTask supports core Twilio operations including sending SMS messages, making voice calls, retrieving call logs, and managing phone numbers. You can automate multi-channel communication workflows through scheduled tasks with full Twilio API integration.

### How do I automate SMS notifications with EasyTask?

Configure your Twilio integration by storing your Account SID and Auth Token in the EasyTask vault, then use the `send_sms` function within a scheduled task. You can trigger notifications based on schedules or workflow events, enabling automated alerting and customer communication.

### Can I schedule recurring calls through EasyTask?

Yes. Use the Twilio integration's call functions within a scheduled task to initiate phone calls at specified intervals. Combined with EasyTask's scheduling engine, you can automate follow-up calls, reminder notifications, and IVR workflows on any schedule.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
