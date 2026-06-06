---
title: Memcached - EasyTask Integration Guide
description: Connect Memcached with EasyTask for automated distributed caching operations. Step-by-step setup, configuration, and best practices.
keywords:
  - memcached
  - easytask
  - workflow orchestration
  - automation
  - distributed caching
  - cache management
---

# Memcached API

The Memcached API provides a set of operations for interacting with Memcached, a distributed memory caching system. It allows users to store, retrieve, and manage cached data.

## Why Integrate Memcached with EasyTask?

Integrating Memcached with EasyTask enables you to automate cache management operations within your workflows. This integration allows you to:

- **Automate Cache Lifecycle Management**: Programmatically set, get, update, and delete cache entries with configurable TTL as part of your automated workflows.
- **Streamline Multi-Key Operations**: Perform batch operations like multi-get, multi-set, and multi-delete to efficiently manage large sets of cached data.
- **Monitor Cache Health**: Retrieve server statistics and manage connections automatically to keep your caching layer running smoothly.

## Required Values in Vault

```
{
    "is_credentials": {
        "userid": "test",
        "passwd": "test123"
    },
    "integrations": {
        "secret": {
            "host": "xxxxxxxx (String Type)",
            "port": "xxxxxxxx (String Type)"
        }
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
        "integration": "memcached",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "memcached/secret"
        },
        "action": [
            {
                "get_stats": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
        {
            "integration": "memcached",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "memcache/server1"
            },
            "error": false,
            "action": [
                {
                    "get_stats": ["10.0.21.106:11211 (0)",
                        {
                            "pid": "1",
                            "uptime": "309794",
                            "time": "1704005487",
                            "version": "1.6.22",
                            "pointer_size": "64",
                            "rusage_user": "36.523994",
                            "rusage_system": "7.480027",
                            "curr_items": "0",
                            "total_items": "12",
                            "bytes": "0",
                            "curr_connections": "2",
                            "total_connections": "11",
                            "connection_structures": "3",
                            "cmd_get": "16",
                            "cmd_set": "12",
                            "get_hits": "14",
                            "get_misses": "2",
                            "evictions": "0",
                            "bytes_read": "1869",
                            "bytes_written": "1621",
                            "limit_maxbytes": "67108864",
                            "threads": "4"
                        }
                    ]
                }
            ]
        }
    
    ```

## Functions

### `get_stats`

**get_stats**: This function retrieves statistics from the Memcached server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing various statistics |

=== "JSON"

    ```json
    {
        "get_stats": {}
    }
    ```

### `flush_all`

**flush_all**: This function flushes all items from the Memcached server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "flush_all": {}
    }
    ```

### `add`

**add**: This function adds a new key-value pair to Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to add | yes |
    | val | any | Value to add | yes |
    | time | int | Expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "add": {
            "key": "test_key",
            "val": 1,
            "time": 1000
        }
    }
    ```

### `set`

**set**: This function sets a key-value pair in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to set | yes |
    | val | any | Value to set | yes |
    | time | int | Expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "set": {
            "key": "test_key2",
            "val": "test_value",
            "time": 100
        }
    }
    ```

### `set_multi`

**set_multi**: This function sets multiple key-value pairs in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | mapping | dict | Dictionary of key-value pairs to set | yes |
    | time | int | Expiration time in seconds | yes |
    | key_prefix | str | Prefix for all keys | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of keys that failed to be set |

=== "JSON"

    ```json
    {
        "set_multi": {
            "mapping": {"key1": "val1", "key2": "val2"},
            "time": 100,
            "key_prefix": "mem"
        }
    }
    ```

### `replace`

**replace**: This function replaces the value of an existing key in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to replace | yes |
    | val | any | New value | yes |
    | time | int | Expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "replace": {
            "key": "test_key2",
            "val": "new_value",
            "time": 100
        }
    }
    ```

### `append`

**append**: This function appends data to an existing key's value in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to append to | yes |
    | val | str | Value to append | yes |
    | time | int | Expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "append": {
            "key": "test_key2",
            "val": "X",
            "time": 100
        }
    }
    ```

### `prepend`

**prepend**: This function prepends data to an existing key's value in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to prepend to | yes |
    | val | str | Value to prepend | yes |
    | time | int | Expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "prepend": {
            "key": "test_key2",
            "val": "X",
            "time": 100
        }
    }
    ```

### `incr`

**incr**: This function increments the value of an existing key in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to increment | yes |
    | delta | int | Amount to increment by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | New value after increment |

=== "JSON"

    ```json
    {
        "incr": {
            "key": "test_key",
            "delta": 1
        }
    }
    ```

### `decr`

**decr**: This function decrements the value of an existing key in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to decrement | yes |
    | delta | int | Amount to decrement by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | New value after decrement |

=== "JSON"

    ```json
    {
        "decr": {
            "key": "test_key",
            "delta": 1
        }
    }
    ```

### `get`

**get**: This function retrieves the value of a key from Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | Value associated with the key |

=== "JSON"

    ```json
    {
        "get": {
            "key": "test_key"
        }
    }
    ```

### `gets`

**gets**: This function retrieves the value and cas id of a key from Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | tuple | Tuple containing the value and cas id |

=== "JSON"

    ```json
    {
        "gets": {
            "key": "test_key"
        }
    }
    ```

### `get_multi`

**get_multi**: This function retrieves multiple values from Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | keys | list | List of keys to retrieve | yes |
    | key_prefix | str | Prefix for all keys | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of key-value pairs |

=== "JSON"

    ```json
    {
        "get_multi": {
            "keys": ["key1", "key2"],
            "key_prefix": "mem"
        }
    }
    ```

### `touch`

**touch**: This function updates the expiry time of a key in Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to update | yes |
    | time | int | New expiration time in seconds | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "touch": {
            "key": "test_key",
            "time": 500
        }
    }
    ```

### `delete`

**delete**: This function deletes a key from Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | key | str | Key to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "delete": {
            "key": "test_key2"
        }
    }
    ```

### `delete_multi`

**delete_multi**: This function deletes multiple keys from Memcached.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | keys | list | List of keys to delete | yes |
    | key_prefix | str | Prefix for all keys | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if all deletions were successful |

=== "JSON"

    ```json
    {
        "delete_multi": {
            "keys": ["key1", "key2"],
            "key_prefix": "mem"
        }
    }
    ```

### `disconnect_all`

**disconnect_all**: This function disconnects from all Memcached servers.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "disconnect_all": {}
    }
    ```

---

## Frequently Asked Questions

### How do I configure Memcached credentials in EasyTask?
Use the EasyTask vault system to securely store your Memcached connection details. Navigate to the integration configuration page and add your server details under a vault key like `memcached/server1`. Include the host and port of your Memcached server.

### Can I use Memcached with both EasyTask Cloud and On-Premises?
Yes, Memcached works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the Memcached server is reachable from the integration server.

### How do I troubleshoot Memcached connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your host and port in the vault, ensure the Memcached server is accessible from the integration server, and test connectivity using the built-in connection test feature. You can also use the `get_stats` function to verify server responsiveness.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
