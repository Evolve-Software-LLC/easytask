---
title: ClickUp - EasyTask Integration Guide
description: Connect ClickUp with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing workspaces, spaces, lists, and tasks.
keywords:
  - clickup
  - easytask
  - workflow orchestration
  - automation
  - project management
  - task management
---

# Clickup API

The Clickup API provides a comprehensive set of endpoints for creating, organizing, and managing workspaces, spaces, lists, and tasks. It also facilitates communication within tasks.

## Why Integrate ClickUp with EasyTask?

Integrating ClickUp with EasyTask enables you to automate project and task management workflows across your organization. This integration allows you to:

- **Automate Task Lifecycle Management**: Create, update, and track ClickUp tasks automatically as part of your EasyTask workflows without manual intervention.
- **Synchronize Workspaces and Spaces**: Keep your ClickUp workspaces, spaces, and lists in sync with other business systems through automated EasyTask orchestration.
- **Streamline Team Communication**: Automatically send and retrieve task comments and messages, keeping your team informed through automated notifications and updates.

## Requirements in Vault

```
{
    "secret": {
        "token": "................."
    }
}
```

## Example Usage

=== "Command"

    ```sh
    curl -X POST http://localhost:8014/run-integration \
    -H "Content-Type: application/json" \
    -d '{
        "is_credentials": {
        "userid": "gAAAAABpYAT5SrWnvJnWWk7OTmNDFSvtwah3t2HuDnbb_G2n69i2De_ra4EItK5TMXYHHLzZPQa_Ll58j8GlYS1S42g9eIxokQ==",
        "passwd": "gAAAAABpYAT5gS7jV8gpcnjr26utcTXxDPnS_mZIVIj4yTxQmdCKr7qdEzCn80ASocsrvURzrgTrMsMq9Ju_GSFC5DZlIOfKQg=="
        },
        "integrations": [
        {
            "integration": "clickup",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
            "vault_path_key": "clickup/secret"
            },
            "action": [
            {
                "get_all_workspaces": {}
            }
            ]
        }
        ]
    }'
  
    ```

=== "Output"

    ```json
    
    {
        "integration": "clickup",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
        "vault_path_key": "clickup/secret"
        },
        "error": false,
        "action": [
        {
            "get_all_workspaces": {
            "test workspace": "90131301776"
            }
        }
        ]
    }

    ```

## Functions

### `get_all_workspaces`

**get_all_workspaces**: This function retrieves all workspaces for the authenticated user.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing workspace information |

=== "JSON"

    ```json
    {
        "get_all_workspaces": {}
    }
    ```

### `get_all_spaces`

**get_all_spaces**: This function retrieves all spaces across all workspaces.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing space information |

=== "JSON"

    ```json
    {
        "get_all_spaces": {}
    }
    ```

### `get_all_lists`

**get_all_lists**: This function retrieves all lists across all spaces.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing list information |

=== "JSON"

    ```json
    {
        "get_all_lists": {}
    }
    ```

### `get_all_tasks`

**get_all_tasks**: This function retrieves all tasks across all lists.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing task information |

=== "JSON"

    ```json
    {
        "get_all_tasks": {}
    }
    ```

### `create_space`

**create_space**: This function creates a new space in a specified workspace.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | workspace_name | str | Name of the workspace to create the space in | yes |
    | space_details | dict | Dictionary containing space details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the created space |

=== "JSON"

    ```json
    {
        "create_space": {
            "workspace_name": "Test WorkSpace",
            "space_details": {
                "name": "testspace"
            }
        }
    }
    ```

### `create_list`

**create_list**: This function creates a new list in a specified space.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | space_name | str | Name of the space to create the list in | yes |
    | list_details | dict | Dictionary containing list details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the created list |

=== "JSON"

    ```json
    {
        "create_list": {
            "space_name": "testspace",
            "list_details": {
                "name": "testlist"
            }
        }
    }
    ```

### `create_task`

**create_task**: This function creates a new task in a specified list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list to create the task in | yes |
    | task_details | dict | Dictionary containing task details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the created task |

=== "JSON"

    ```json
    {
        "create_task": {
            "list_name": "testlist",
            "task_details": {
                "name": "Test Task",
                "description": "Test Task Description"
            }
        }
    }
    ```

### `update_space`

**update_space**: This function updates an existing space.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | space_name | str | Name of the space to update | yes |
    | space_details | dict | Dictionary containing updated space details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the updated space |

=== "JSON"

    ```json
    {
        "update_space": {
            "space_name": "testspace",
            "space_details": {
                "name": "New Test Space"
            }
        }
    }
    ```

### `update_list`

**update_list**: This function updates an existing list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list to update | yes |
    | list_details | dict | Dictionary containing updated list details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the updated list |

=== "JSON"

    ```json
    {
        "update_list": {
            "list_name": "testlist",
            "list_details": {
                "name": "New Test List"
            }
        }
    }
    ```

### `update_task`

**update_task**: This function updates an existing task.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | task_name | str | Name of the task to update | yes |
    | task_details | dict | Dictionary containing updated task details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the updated task |

=== "JSON"

    ```json
    {
        "update_task": {
            "task_name": "Test Task",
            "task_details": {
                "name": "newtesttask",
                "tast_details": "New Test Task Description"
            }
        }
    }
    ```

### `send_message`

**send_message**: This function sends a message (comment) to a specific task.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | task_name | str | Name of the task to send the message to | yes |
    | message | str | Content of the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the sent message |

=== "JSON"

    ```json
    {
        "send_message": {
            "task_name": "newtesttask",
            "message": "Test Message"
        }
    }
    ```

### `retreive_message`

**retreive_message**: This function retrieves messages (comments) from a specific task.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | task_name | str | Name of the task to retrieve messages from | yes |
    | num | int | Number of messages to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing message information |

=== "JSON"

    ```json
    {
        "retreive_message": {
            "task_name": "newtesttask",
            "num": 1
        }
    }
    ```

### `modify_message`

**modify_message**: This function modifies an existing message (comment).

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | comment_id | str | ID of the comment to modify | yes |
    | message | str | Updated content of the message | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing information about the modified message |

=== "JSON"

    ```json
    {
        "modify_message": {
            "comment_id": "123456789",
            "message": "Updated message content"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure ClickUp credentials in EasyTask?
Use the EasyTask vault system to securely store your ClickUp API token. Navigate to the integration configuration page and add your token under a vault key like `clickup/secret`.

### Can I use ClickUp with both EasyTask Cloud and On-Premises?
Yes, ClickUp works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical since ClickUp is a cloud-based service.

### How do I troubleshoot ClickUp connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your API token in the vault, ensure the ClickUp API is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
