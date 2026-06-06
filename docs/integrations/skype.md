---
title: Skype - EasyTask Integration Guide
description: Connect Skype with EasyTask for automated messaging and communication workflows. Step-by-step setup, configuration, and best practices for Skype integration.
keywords:
  - skype
  - easytask
  - workflow orchestration
  - automation
  - messaging
  - communication
---

# Skype

Skype is software that enables the world's conversations. Millions of individuals and businesses use Skype to make free video and voice one-to-one and group calls, send instant messages and share files with other people on Skype.

## Why Integrate Skype with EasyTask?

Integrating Skype with EasyTask enables you to automate messaging and communication workflows. This integration allows you to:

- **Automate Message Workflows**: Send, edit, delete, and retrieve messages programmatically as part of notification and alerting pipelines.
- **Manage Contacts and Groups**: Automatically create group chats, manage members and admins, and retrieve contact lists for streamlined communication.
- **Handle File Transfers**: Send files and images through Skype automatically as part of document distribution and reporting workflows.

## Integration Server Vault details

### Required values in Vault

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": {
        "secret": {
          "password": "**********",
          "token_file_name": "",
          "username": "example123@gmail.com"
        }
      }
    }
    ```

### Credentials for logging in

| Key | Description |
|-----|-------------|
| Username | The username you use to log into Skype |
| Password | The password you use to log into Skype |

`Use the same username and password that you use to login into Skype.`

### Skype Integration JSON Format

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "skype") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing Skype credentials | Yes |
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
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of Skype 

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
            {
                "integration": "skype",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "skype/server1"
                },
                "action": [
                    {
                        "create_group": {
                            "g_members": [""],
                            "g_admins": [""]
                        }
                    }
                ]
            }
        ]
      }'

    ```

=== "Output"

    ```json
    {
        {
            "g_members": [""],
            "g_admins": [""]
        }
    }
    ```

## Functions

### `login`

**Logging In**:

This function authenticates the user with Skype using credentials stored in the vault. It creates a new file containing the authentication token for future logins.

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
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "login": {}
            }
          ]
        }
      ]
    }
    ```

### `logout`

**Logging Out**:

This function logs out the user from Skype and deletes the authentication file created during login.

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
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "logout": {}
            }
          ]
        }
      ]
    }
    ```

### `get_contacts`

**Contacts of a user**:

This function retrieves the user's contacts and returns a SkypeContacts object containing details of all contacts.

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
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "get_contacts": {}
            }
          ]
        }
      ]
    }
    ```

### `block_user`

**Blocking a User**:

This function blocks a specified user on Skype.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | uid | string | User ID of the user to be blocked | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "block_user": {
                "uid": "live:asadnizami123"
              }
            }
          ]
        }
      ]
    }
    ```

### `unblock_user`

**Unblocking a User**:

This function unblocks a previously blocked user on Skype.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | uid | string | User ID of the user to be unblocked | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "unblock_user": {
                "uid": "live:asadnizami123"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_chats`

**Conversations**:

This function retrieves a list of recent chats for the user.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | chat_num | integer | Number of recent chats to fetch | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "get_chats": {
                "chat_num": 5
              }
            }
          ]
        }
      ]
    }
    ```

### `create_group`

**Creating a Group Chat**:

This function creates a new group chat and returns a SkypeGroupChat object for the newly created group.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | g_members | array | List of user IDs to be added as members | Yes |
    | g_admins | array | List of user IDs to be added as admins | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "create_group": {
                "g_members": [""],
                "g_admins": [""]
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_chat`

**Deleting a conversation**:

This function deletes a specified chat in Skype.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | chat_id | string | The ID of the chat to be deleted | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "delete_chat": {
                "chat_id": "8:live:asadnizami123"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_msg`

**Sending Messages**:

This function sends a message to a specified chat. It returns a SkypeMsg object of the sent message.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | chat_id | string | The ID of the chat to send the message to | Yes |
    | msg | string | The message to be sent | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "send_msg": {
                "chat_id": "8:live:asadnizami123",
                "msg": "test message from json"
              }
            }
          ]
        }
      ]
    }
    ```

### `send_file`

**Sending Files**:

This function sends a file to a specified chat. It returns a SkypeFileMsg object of the sent file.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | chat_id | string | The ID of the chat to send the file to | Yes |
    | file | string | The path of the file to be sent | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "send_file": {
                "chat_id": "8:live:asadnizami123",
                "file": ""
              }
            }
          ]
        }
      ]
    }
    ```

Note: If the file is an image, setting `image=True` in the send_file method would create a thumbnail of that image.

### `edit_msg`

**Editing a message**:

This function edits a previously sent message in Skype.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | msg | string | The original message to be edited | Yes |
    | content | string | The new content for the message | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "edit_msg": {
                "msg": "Hello",
                "content": "Hey"
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_msg`

**Deleting a message**:

This function deletes a specified message in Skype.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | msg | string | The message to be deleted | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "delete_msg": {
                "msg": "Hello"
              }
            }
          ]
        }
      ]
    }
    ```

Note: Messages can be undeleted by editing their content to be non-empty.

### `retrieve_msg`

**Retrieving messages**:

This function fetches recent messages from a specified conversation. It returns a list of SkypeMsg objects.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | chat_id | string | The ID of the chat to retrieve messages from | Yes |
    | msg_num | integer | The number of recent messages to retrieve | Yes |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "skype",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "skype/server1"
          },
          "action": [
            {
              "retrieve_msg": {
                "chat_id": "8:live:asadnizami123",
                "msg_num": 2
              }
            }
          ]
        }
      ]
    }
    ```

---

## Frequently Asked Questions

### How do I configure Skype credentials in EasyTask?
Use the EasyTask vault system to securely store your Skype login credentials. Navigate to the integration configuration page and add your server details under a vault key like `skype/server1`. Include your Skype username and password — the same credentials you use to log into Skype.

### Can I use Skype with both EasyTask Cloud and On-Premises?
Yes, Skype works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the integration server has network access to Skype services.

### How do I troubleshoot Skype connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your Skype username and password in the vault, ensure the integration server can reach Skype's network endpoints, and try using the `login` function to test authentication. If a token file is used, verify the file path is correct and accessible.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
