---
title: Hazelcast - EasyTask Integration Guide
description: Connect Hazelcast with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing distributed data structures.
keywords:
  - hazelcast
  - easytask
  - workflow orchestration
  - automation
  - in-memory data grid
  - distributed computing
---

# Hazelcast API

The Hazelcast API provides a set of operations for managing distributed data structures such as lists, sets, queues, maps, and ring buffers. It allows users to interact with these data structures programmatically in a distributed environment.

## Why Integrate Hazelcast with EasyTask?

Integrating Hazelcast with EasyTask enables you to automate distributed in-memory data management workflows. This integration allows you to:

- **Manage Distributed Data Structures**: Automate operations on lists, sets, queues, maps, and ring buffers across your Hazelcast cluster through EasyTask orchestration.
- **Scale Data Processing**: Leverage Hazelcast's in-memory data grid to handle high-throughput data operations as part of your automated EasyTask workflows.
- **Streamline Cluster Operations**: Connect to Hazelcast clusters, manage distributed collections, and shutdown connections programmatically without manual intervention.

## Required Values in Vault

```
{
"secret": {
    "cluster_members": [
    "xxx.xxx.xxx.xxx:xxxxx",
    "xxx.xxx.xxx.xxx:xxxxx"
    ]
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
        "integration": "hazelcast",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "hazelcast/secret"
        },
        "action": [
            {
                "add_to_list": {
                    "list_name": "json_list",
                    "item": 1
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "user": "test user",
        "integration": "hazelcast",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "hazelcast/server1"
        },
        "error": false,
        "action": [
            {
                "add_to_list": true
            }
        ]
    }

    ```

## Functions

### List Operations

#### `add_to_list`

**add_to_list**: This function adds an item to a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | item | any | Item to add to the list | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was added successfully |

=== "JSON"

    ```json
    {
        "add_to_list": {
            "list_name": "json_list",
            "item": 1
        }
    }
    ```

#### `add_all_to_list`

**add_all_to_list**: This function adds multiple items to a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | items | list | List of items to add | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items were added successfully |

=== "JSON"

    ```json
    {
        "add_all_to_list": {
            "list_name": "json_list",
            "items": [2, 3, 5]
        }
    }
    ```

#### `add_at_to_list`

**add_at_to_list**: This function adds an item to a list at a specific index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | index | int | Index at which to add the item | yes |
    | item | any | Item to add to the list | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was added successfully |

=== "JSON"

    ```json
    {
        "add_at_to_list": {
            "list_name": "json_list",
            "index": 3,
            "item": 4
        }
    }
    ```

#### `add_all_at_list`

**add_all_at_list**: This function adds multiple items to a list at a specific index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | index | int | Index at which to add the items | yes |
    | items | list | List of items to add | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items were added successfully |

=== "JSON"

    ```json
    {
        "add_all_at_list": {
            "list_name": "json_list",
            "index": 5,
            "items": [1, 2, 4, 3, 5, 6]
        }
    }
    ```

#### `get_from_list`

**get_from_list**: This function retrieves an item from a list at a specific index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | index | int | Index of the item to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The item at the specified index |

=== "JSON"

    ```json
    {
        "get_from_list": {
            "list_name": "json_list",
            "index": 0
        }
    }
    ```

#### `get_all_from_list`

**get_all_from_list**: This function retrieves all items from a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | All items in the list |

=== "JSON"

    ```json
    {
        "get_all_from_list": {
            "list_name": "json_list"
        }
    }
    ```

#### `get_sub_list`

**get_sub_list**: This function retrieves a sublist from a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | from_index | int | Start index of the sublist | yes |
    | to_index | int | End index of the sublist | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | Sublist of items |

=== "JSON"

    ```json
    {
        "get_sub_list": {
            "list_name": "json_list",
            "from_index": 1,
            "to_index": 3
        }
    }
    ```

#### `first_index_in_list`

**first_index_in_list**: This function finds the first index of an item in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | item | any | Item to find | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | First index of the item, or -1 if not found |

=== "JSON"

    ```json
    {
        "first_index_in_list": {
            "list_name": "json_list",
            "item": 1
        }
    }
    ```

#### `last_index_in_list`

**last_index_in_list**: This function finds the last index of an item in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | item | any | Item to find | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Last index of the item, or -1 if not found |

=== "JSON"

    ```json
    {
        "last_index_in_list": {
            "list_name": "json_list",
            "item": 2
        }
    }
    ```

#### `is_value_in_list`

**is_value_in_list**: This function checks if a value is in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | item | any | Item to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item is in the list, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_list": {
            "list_name": "json_list",
            "item": 1
        }
    }
    ```

#### `is_all_value_in_list`

**is_all_value_in_list**: This function checks if all specified values are in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | items | list | List of items to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items are in the list, False otherwise |

=== "JSON"

    ```json
    {
        "is_all_value_in_list": {
            "list_name": "json_list",
            "items": [1, 2]
        }
    }
    ```

#### `replace_in_list`

**replace_in_list**: This function replaces an item at a specific index in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | index | int | Index of the item to replace | yes |
    | item | any | New item to put at the index | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous item at the index |

=== "JSON"

    ```json
    {
        "replace_in_list": {
            "list_name": "json_list",
            "index": 1,
            "item": 1
        }
    }
    ```

#### `retain_all_in_list`

**retain_all_in_list**: This function retains only the specified items in a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | items | list | List of items to retain | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the list changed as a result of the call |

=== "JSON"

    ```json
    {
        "retain_all_in_list": {
            "list_name": "json_list",
            "items": [1, 2, 3, 4]
        }
    }
    ```

#### `remove_from_list`

**remove_from_list**: This function removes the first occurrence of an item from a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | item | any | Item to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was removed, False otherwise |

=== "JSON"

    ```json
    {
        "remove_from_list": {
            "list_name": "json_list",
            "item": 1
        }
    }
    ```

#### `remove_at_from_list`

**remove_at_from_list**: This function removes an item at a specific index from a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | index | int | Index of the item to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The removed item |

=== "JSON"

    ```json
    {
        "remove_at_from_list": {
            "list_name": "json_list",
            "index": 0
        }
    }
    ```

#### `remove_all_from_list`

**remove_all_from_list**: This function removes all occurrences of specified items from a list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | list_name | str | Name of the list | yes |
    | items | list | List of items to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the list changed as a result of the call |

=== "JSON"

    ```json
    {
        "remove_all_from_list": {
            "list_name": "json_list",
            "items": [4, 3]
        }
    }
    ```

### Set Operations

#### `add_to_set`

**add_to_set**: This function adds an item to a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | item | any | Item to add to the set | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was added successfully |

=== "JSON"

    ```json
    {
        "add_to_set": {
            "set_name": "json_set",
            "item": 1
        }
    }
    ```

#### `add_all_to_set`

**add_all_to_set**: This function adds multiple items to a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | items | list | List of items to add | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items were added successfully |

=== "JSON"

    ```json
    {
        "add_all_to_set": {
            "set_name": "json_set",
            "items": [2, 3, 4, 5]
        }
    }
    ```

#### `get_all_from_set`

**get_all_from_set**: This function retrieves all items from a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | All items in the set |

=== "JSON"

    ```json
    {
        "get_all_from_set": {
            "set_name": "json_set"
        }
    }
    ```

#### `is_value_in_set`

**is_value_in_set**: This function checks if a value is in a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | item | any | Item to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item is in the set, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_set": {
            "set_name": "json_set",
            "item": 1
        }
    }
    ```

#### `is_all_value_in_set`

**is_all_value_in_set**: This function checks if all specified values are in a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | items | list | List of items to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items are in the set, False otherwise |

=== "JSON"

    ```json
    {
        "is_all_value_in_set": {
            "set_name": "json_set",
            "items": [1, 2, 3, 4, 5]
        }
    }
    ```

#### `retain_all_in_set`

**retain_all_in_set**: This function retains only the specified items in a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | items | list | List of items to retain | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the set changed as a result of the call |

=== "JSON"

    ```json
    {
        "retain_all_in_set": {
            "set_name": "json_set",
            "items": [1, 2, 3]
        }
    }
    ```

#### `remove_from_set`

**remove_from_set**: This function removes an item from a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | item | any | Item to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was removed, False otherwise |

=== "JSON"

    ```json
    {
        "remove_from_set": {
            "set_name": "json_set",
            "item": 1
        }
    }
    ```

#### `remove_all_from_set`

**remove_all_from_set**: This function removes all occurrences of specified items from a set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | set_name | str | Name of the set | yes |
    | items | list | List of items to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the set changed as a result of the call |

=== "JSON"

    ```json
    {
        "remove_all_from_set": {
            "set_name": "json_set",
            "items": [2, 3]
        }
    }
    ```

### Queue Operations

#### `add_to_queue`

**add_to_queue**: This function adds an item to a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | item | any | Item to add to the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was added successfully |

=== "JSON"

    ```json
    {
        "add_to_queue": {
            "queue_name": "json_queue",
            "item": 1
        }
    }
    ```

#### `add_all_to_queue`

**add_all_to_queue**: This function adds multiple items to a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | items | list | List of items to add | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items were added successfully |

=== "JSON"

    ```json
    {
        "add_all_to_queue": {
            "queue_name": "json_queue",
            "items": [2, 3, 4, 5, 1, 2]
        }
    }
    ```

#### `get_all_from_queue`

**get_all_from_queue**: This function retrieves all items from a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | All items in the queue |

=== "JSON"

    ```json
    {
        "get_all_from_queue": {
            "queue_name": "json_queue"
        }
    }
    ```

#### `put_in_queue`

**put_in_queue**: This function puts an item into a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | item | any | Item to put in the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was put successfully |

=== "JSON"

    ```json
    {
        "put_in_queue": {
            "queue_name": "json_queue",
            "item": 1
        }
    }
    ```

#### `is_value_in_queue`

**is_value_in_queue**: This function checks if a value is in a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | item | any | Item to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item is in the queue, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_queue": {
            "queue_name": "json_queue",
            "item": 1
        }
    }
    ```

#### `is_all_value_in_queue`

**is_all_value_in_queue**: This function checks if all specified values are in a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | items | list | List of items to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all items are in the queue, False otherwise |

=== "JSON"

    ```json
    {
        "is_all_value_in_queue": {
            "queue_name": "json_queue",
            "items": [1, 2, 3, 4, 5]
        }
    }
    ```

#### `retain_all_in_queue`

**retain_all_in_queue**: This function retains only the specified items in a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | items | list | List of items to retain | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the queue changed as a result of the call |

=== "JSON"

    ```json
    {
        "retain_all_in_queue": {
            "queue_name": "json_queue",
            "items": [1, 2, 3]
        }
    }
    ```

#### `remove_from_queue`

**remove_from_queue**: This function removes an item from a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | item | any | Item to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was removed, False otherwise |

=== "JSON"

    ```json
    {
        "remove_from_queue": {
            "queue_name": "json_queue",
            "item": 1
        }
    }
    ```

#### `remove_all_from_queue`

**remove_all_from_queue**: This function removes all occurrences of specified items from a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | items | list | List of items to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the queue changed as a result of the call |

=== "JSON"

    ```json
    {
        "remove_all_from_queue": {
            "queue_name": "json_queue",
            "items": [2, 3]
        }
    }
    ```

#### `offer`

**offer**: This function offers an item to a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | item | any | Item to offer to the queue | yes |
    | timeout | int | Timeout in milliseconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the item was offered successfully |

=== "JSON"

    ```json
    {
        "offer": {
            "queue_name": "json_queue",
            "item": 2,
            "timeout": 0
        }
    }
    ```

#### `poll`

**poll**: This function retrieves and removes the head of a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |
    | timeout | int | Timeout in milliseconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The head of the queue, or null if the queue is empty |

=== "JSON"

    ```json
    {
        "poll": {
            "queue_name": "json_queue",
            "timeout": 0
        }
    }
    ```

#### `peek`

**peek**: This function retrieves, but does not remove, the head of a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The head of the queue, or null if the queue is empty |

=== "JSON"

    ```json
    {
        "peek": {
            "queue_name": "json_queue"
        }
    }
    ```

#### `take`

**take**: This function retrieves and removes the head of a queue, waiting if necessary until an element becomes available.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The head of the queue |

=== "JSON"

    ```json
    {
        "take": {
            "queue_name": "json_queue"
        }
    }
    ```

#### `rem_cap_queue`

**rem_cap_queue**: This function retrieves the remaining capacity of a queue.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | queue_name | str | Name of the queue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The remaining capacity of the queue |

=== "JSON"

    ```json
    {
        "rem_cap_queue": {
            "queue_name": "json_queue"
        }
    }
    ```

### Ring Buffer Operations

#### `add_to_rbuf`

**add_to_rbuf**: This function adds an item to a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |
    | item | any | Item to add to the ring buffer | yes |
    | overflow_policy | int | Overflow policy (0-4) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The sequence of the added item |

=== "JSON"

    ```json
    {
        "add_to_rbuf": {
            "buf_name": "json_rbuf",
            "item": 1,
            "overflow_policy": 0
        }
    }
    ```

#### `add_all_to_rbuf`

**add_all_to_rbuf**: This function adds multiple items to a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |
    | items | list | List of items to add | yes |
    | overflow_policy | int | Overflow policy (0-4) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The sequence of the last added item |

=== "JSON"

    ```json
    {
        "add_all_to_rbuf": {
            "buf_name": "json_rbuf",
            "items": [2, 3, 4, 5],
            "overflow_policy": 0
        }
    }
    ```

#### `capacity_rbuf`

**capacity_rbuf**: This function retrieves the capacity of a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The capacity of the ring buffer |

=== "JSON"

    ```json
    {
        "capacity_rbuf": {
            "buf_name": "json_rbuf"
        }
    }
    ```

#### `tail_sequence`

**tail_sequence**: This function retrieves the tail sequence of a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The tail sequence of the ring buffer |

=== "JSON"

    ```json
    {
        "tail_sequence": {
            "buf_name": "json_rbuf"
        }
    }
    ```

#### `head_sequence`

**head_sequence**: This function retrieves the head sequence of a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The head sequence of the ring buffer |

=== "JSON"

    ```json
    {
        "head_sequence": {
            "buf_name": "json_rbuf"
        }
    }
    ```

#### `rem_cap_rbuf`

**rem_cap_rbuf**: This function retrieves the remaining capacity of a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | The remaining capacity of the ring buffer |

=== "JSON"

    ```json
    {
        "rem_cap_rbuf": {
            "buf_name": "json_rbuf"
        }
    }
    ```

#### `read_one_from_rbuf`

**read_one_from_rbuf**: This function reads one item from a ring buffer at a specific sequence.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |
    | sequence | int | Sequence number to read from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The item at the specified sequence |

=== "JSON"

    ```json
    {
        "read_one_from_rbuf": {
            "buf_name": "json_rbuf",
            "sequence": 1
        }
    }
    ```

#### `read_many_from_rbuf`

**read_many_from_rbuf**: This function reads multiple items from a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |
    | start_sequence | int | Starting sequence number | yes |
    | min_count | int | Minimum number of items to read | yes |
    | max_count | int | Maximum number of items to read | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of items read from the ring buffer |

=== "JSON"

    ```json
    {
        "read_many_from_rbuf": {
            "buf_name": "json_rbuf",
            "start_sequence": 1,
            "min_count": 1,
            "max_count": 2
        }
    }
    ```

#### `destory_rbuf`

**destory_rbuf**: This function destroys a ring buffer.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | buf_name | str | Name of the ring buffer | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the ring buffer was destroyed successfully |

=== "JSON"

    ```json
    {
        "destory_rbuf": {
            "buf_name": "json_rbuf"
        }
    }
    ```

### Map Operations

#### `put_in_map`

**put_in_map**: This function puts a key-value pair into a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to insert | yes |
    | value | any | Value to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous value associated with the key, or null if there was no mapping for the key |

=== "JSON"

    ```json
    {
        "put_in_map": {
            "map_name": "json_map",
            "key": "key",
            "value": "val"
        }
    }
    ```

#### `put_all_in_map`

**put_all_in_map**: This function puts multiple key-value pairs into a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | map | dict | Dictionary of key-value pairs to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "put_all_in_map": {
            "map_name": "json_map",
            "map": {
                "key1": "val1",
                "key2": "val2",
                "key3": "val3"
            }
        }
    }
    ```

#### `is_value_in_map`

**is_value_in_map**: This function checks if a value is in a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | value | any | Value to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the value is in the map, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_map": {
            "map_name": "json_map",
            "value": "val"
        }
    }
    ```

#### `is_key_in_map`

**is_key_in_map**: This function checks if a key is in a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the key is in the map, False otherwise |

=== "JSON"

    ```json
    {
        "is_key_in_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `replace_in_map`

**replace_in_map**: This function replaces the value for a given key in a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to replace | yes |
    | value | any | New value | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous value associated with the key, or null if there was no mapping for the key |

=== "JSON"

    ```json
    {
        "replace_in_map": {
            "map_name": "json_map",
            "key": "key",
            "value": "new_val"
        }
    }
    ```

#### `replace_if_same_in_map`

**replace_if_same_in_map**: This function replaces the value for a given key in a map if the current value matches the expected value.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to replace | yes |
    | old_value | any | Expected current value | yes |
    | new_value | any | New value | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the value was replaced, False otherwise |

=== "JSON"

    ```json
    {
        "replace_if_same_in_map": {
            "map_name": "json_map",
            "key": "key",
            "old_value": "new_val",
            "new_value": "new_value"
        }
    }
    ```

#### `get_map`

**get_map**: This function gets the value for a given key from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to get | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The value associated with the key, or null if the key is not found |

=== "JSON"

    ```json
    {
        "get_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `get_all_tuples_map`

**get_all_tuples_map**: This function gets all key-value pairs from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of all key-value pairs in the map |

=== "JSON"

    ```json
    {
        "get_all_tuples_map": {
            "map_name": "json_map"
        }
    }
    ```

#### `get_key_list_map`

**get_key_list_map**: This function gets all keys from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all keys in the map |

=== "JSON"

    ```json
    {
        "get_key_list_map": {
            "map_name": "json_map"
        }
    }
    ```

#### `get_value_list_map`

**get_value_list_map**: This function gets all values from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all values in the map |

=== "JSON"

    ```json
    {
        "get_value_list_map": {
            "map_name": "json_map"
        }
    }
    ```

#### `remove_from_map`

**remove_from_map**: This function removes a key-value pair from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous value associated with the key, or null if there was no mapping for the key |

=== "JSON"

    ```json
    {
        "remove_from_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `remove_if_same_from_map`

**remove_if_same_from_map**: This function removes a key-value pair from a map if the current value matches the expected value.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to remove | yes |
    | value | any | Expected value | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the entry was removed, False otherwise |

=== "JSON"

    ```json
    {
        "remove_if_same_from_map": {
            "map_name": "json_map",
            "key": "key2",
            "value": "val2"
        }
    }
    ```

#### `delete_from_map`

**delete_from_map**: This function deletes a key-value pair from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the entry was deleted, False otherwise |

=== "JSON"

    ```json
    {
        "delete_from_map": {
            "map_name": "json_map",
            "key": "key1"
        }
    }
    ```

#### `evict_from_map`

**evict_from_map**: This function evicts a key-value pair from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to evict | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the entry was evicted, False otherwise |

=== "JSON"

    ```json
    {
        "evict_from_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `evict_all_map`

**evict_all_map**: This function evicts all entries from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "evict_all_map": {
            "map_name": "json_map"
        }
    }
    ```

#### `get_all_map`

**get_all_map**: This function gets multiple entries from a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | keys | list | List of keys to get | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of key-value pairs for the requested keys |

=== "JSON"

    ```json
    {
        "get_all_map": {
            "map_name": "json_map",
            "keys": ["key1", "key2"]
        }
    }
    ```

#### `set_in_map`

**set_in_map**: This function sets a value for a key in a map without returning the old value.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to set | yes |
    | value | any | Value to set | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "set_in_map": {
            "map_name": "json_map",
            "key": "key",
            "value": "val"
        }
    }
    ```

#### `lock_in_map`

**lock_in_map**: This function acquires the lock for the specified key in a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to lock | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the lock was acquired |

=== "JSON"

    ```json
    {
        "lock_in_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `is_locked_in_map`

**is_locked_in_map**: This function checks if the lock for the specified key in a map is locked.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the key is locked, False otherwise |

=== "JSON"

    ```json
    {
        "is_locked_in_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

#### `unlock_in_map`

**unlock_in_map**: This function releases the lock for the specified key in a map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the map | yes |
    | key | str | Key to unlock | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the lock was released |

=== "JSON"

    ```json
    {
        "unlock_in_map": {
            "map_name": "json_map",
            "key": "key"
        }
    }
    ```

### MultiMap Operations

#### `put_in_mmap`

**put_in_mmap**: This function puts a key-value pair into a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to insert | yes |
    | value | any | Value to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "put_in_mmap": {
            "map_name": "json_mmap",
            "key": "key",
            "value": "val"
        }
    }
    ```

#### `is_value_in_mmap`

**is_value_in_mmap**: This function checks if a value is in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | value | any | Value to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the value is in the multimap, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_mmap": {
            "map_name": "json_mmap",
            "value": "val"
        }
    }
    ```

#### `is_key_in_mmap`

**is_key_in_mmap**: This function checks if a key is in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the key is in the multimap, False otherwise |

=== "JSON"

    ```json
    {
        "is_key_in_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `get_mmap`

**get_mmap**: This function gets all values associated with a key from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to get | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of values associated with the key |

=== "JSON"

    ```json
    {
        "get_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `get_all_tuples_mmap`

**get_all_tuples_mmap**: This function gets all key-value pairs from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of all key-value pairs in the multimap |

=== "JSON"

    ```json
    {
        "get_all_tuples_mmap": {
            "map_name": "json_mmap"
        }
    }
    ```

#### `get_key_list_mmap`

**get_key_list_mmap**: This function gets all keys from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all keys in the multimap |

=== "JSON"

    ```json
    {
        "get_key_list_mmap": {
            "map_name": "json_mmap"
        }
    }
    ```

#### `get_value_list_mmap`

**get_value_list_mmap**: This function gets all values from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all values in the multimap |

=== "JSON"

    ```json
    {
        "get_value_list_mmap": {
            "map_name": "json_mmap"
        }
    }
    ```

#### `remove_from_mmap`

**remove_from_mmap**: This function removes a key-value pair from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to remove | yes |
    | value | any | Value to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the entry was removed, False otherwise |

=== "JSON"

    ```json
    {
        "remove_from_mmap": {
            "map_name": "json_mmap",
            "key": "key1",
            "value": "val1"
        }
    }
    ```

#### `remove_all_mmap`

**remove_all_mmap**: This function removes all values associated with a key from a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of removed values |

=== "JSON"

    ```json
    {
        "remove_all_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `is_entry_in_mmap`

**is_entry_in_mmap**: This function checks if a key-value pair exists in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to check | yes |
    | value | any | Value to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the entry exists, False otherwise |

=== "JSON"

    ```json
    {
        "is_entry_in_mmap": {
            "map_name": "json_mmap",
            "key": "key",
            "value": "val"
        }
    }
    ```

#### `lock_in_mmap`

**lock_in_mmap**: This function acquires the lock for the specified key in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to lock | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the lock was acquired |

=== "JSON"

    ```json
    {
        "lock_in_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `is_locked_in_mmap`

**is_locked_in_mmap**: This function checks if the lock for the specified key in a multimap is locked.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the key is locked, False otherwise |

=== "JSON"

    ```json
    {
        "is_locked_in_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `unlock_in_mmap`

**unlock_in_mmap**: This function releases the lock for the specified key in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to unlock | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the lock was released |

=== "JSON"

    ```json
    {
        "unlock_in_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `value_count_in_mmap`

**value_count_in_mmap**: This function gets the number of values associated with a key in a multimap.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the multimap | yes |
    | key | str | Key to count values for | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Number of values associated with the key |

=== "JSON"

    ```json
    {
        "value_count_in_mmap": {
            "map_name": "json_mmap",
            "key": "key"
        }
    }
    ```

#### `put_in_rmap`

**put_in_rmap**: This function puts a key-value pair into a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | key | str | Key to insert | yes |
    | value | any | Value to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous value associated with the key, or null if there was no mapping for the key |

=== "JSON"

    ```json
    {
        "put_in_rmap": {
            "map_name": "json_rmap",
            "key": "key",
            "value": "val"
        }
    }
    ```

#### `put_all_in_rmap`

**put_all_in_rmap**: This function puts multiple key-value pairs into a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | source | dict | Dictionary of key-value pairs to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "put_all_in_rmap": {
            "map_name": "json_rmap",
            "source": {
                "key1": "val1",
                "key2": "val2"
            }
        }
    }
    ```

#### `is_value_in_rmap`

**is_value_in_rmap**: This function checks if a value is in a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | value | any | Value to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the value is in the replicated map, False otherwise |

=== "JSON"

    ```json
    {
        "is_value_in_rmap": {
            "map_name": "json_rmap",
            "value": "val"
        }
    }
    ```

#### `is_key_in_rmap`

**is_key_in_rmap**: This function checks if a key is in a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | key | str | Key to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the key is in the replicated map, False otherwise |

=== "JSON"

    ```json
    {
        "is_key_in_rmap": {
            "map_name": "json_rmap",
            "key": "key"
        }
    }
    ```

#### `get_rmap`

**get_rmap**: This function gets the value for a given key from a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | key | str | Key to get | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The value associated with the key, or null if the key is not found |

=== "JSON"

    ```json
    {
        "get_rmap": {
            "map_name": "json_rmap",
            "key": "key"
        }
    }
    ```

#### `get_all_tuples_rmap`

**get_all_tuples_rmap**: This function gets all key-value pairs from a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of all key-value pairs in the replicated map |

=== "JSON"

    ```json
    {
        "get_all_tuples_rmap": {
            "map_name": "json_rmap"
        }
    }
    ```

#### `get_key_list_rmap`

**get_key_list_rmap**: This function gets all keys from a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all keys in the replicated map |

=== "JSON"

    ```json
    {
        "get_key_list_rmap": {
            "map_name": "json_rmap"
        }
    }
    ```
#### `get_value_list_rmap`

**get_value_list_rmap**: This function gets all values from a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all values in the replicated map |

=== "JSON"

    ```json
    {
        "get_value_list_rmap": {
            "map_name": "json_rmap"
        }
    }
    ```

#### `remove_from_rmap`

**remove_from_rmap**: This function removes a key-value pair from a replicated map.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | map_name | str | Name of the replicated map | yes |
    | key | str | Key to remove | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The previous value associated with the key, or null if there was no mapping for the key |

=== "JSON"

    ```json
    {
        "remove_from_rmap": {
            "map_name": "json_rmap",
            "key": "key"
        }
    }
    ```

#### `size`

**size**: This function returns the size of a data structure.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | ds_type | str | Type of data structure (e.g., "LIST") | yes |
    | ds_name | str | Name of the data structure | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Size of the data structure |

=== "JSON"

    ```json
    {
        "size": {
            "ds_type": "LIST",
            "ds_name": "json_list"
        }
    }
    ```

#### `clear`

**clear**: This function clears all elements from a data structure.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | ds_type | str | Type of data structure (e.g., "LIST") | yes |
    | ds_name | str | Name of the data structure | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "clear": {
            "ds_type": "LIST",
            "ds_name": "json_list"
        }
    }
    ```

#### `is_empty`

**is_empty**: This function checks if a data structure is empty.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | ds_type | str | Type of data structure (e.g., "LIST") | yes |
    | ds_name | str | Name of the data structure | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the data structure is empty, False otherwise |

=== "JSON"

    ```json
    {
        "is_empty": {
            "ds_type": "LIST",
            "ds_name": "json_list"
        }
    }
    ```

#### `shutdown`

**shutdown**: This function shuts down the Hazelcast client.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the shutdown was successful |

=== "JSON"

    ```json
    {
        "shutdown": {}
    }
    ```

---

## Frequently Asked Questions

### How do I configure Hazelcast credentials in EasyTask?
Use the EasyTask vault system to securely store your Hazelcast cluster connection details. Navigate to the integration configuration page and add your cluster member addresses under a vault key like `hazelcast/secret`.

### Can I use Hazelcast with both EasyTask Cloud and On-Premises?
Yes, Hazelcast works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot Hazelcast connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your cluster member addresses in the vault, ensure the Hazelcast cluster nodes are accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
