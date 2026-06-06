---
title: Apache Ignite - EasyTask Integration Guide
description: Connect Apache Ignite with EasyTask for automated distributed cache and SQL operations. Step-by-step setup, configuration, and best practices.
keywords:
  - apache ignite
  - ignite
  - easytask
  - workflow orchestration
  - automation
  - distributed cache
---

# Ignite API

The Ignite API provides a set of operations for interacting with Apache Ignite caches and performing SQL operations. It allows users to store, retrieve, and manage data in a distributed cache system.

## Why Integrate Apache Ignite with EasyTask?

Integrating Apache Ignite with EasyTask enables you to automate distributed cache management and SQL operations within your workflows. This integration allows you to:

- **Automate Cache Operations**: Programmatically put, get, and scan cache entries across your Ignite cluster without manual intervention.
- **Execute SQL at Scale**: Run SQL commands against your distributed data grid as part of automated workflow steps.
- **Centralize Cluster Configuration**: Store Ignite host and port details securely in the EasyTask vault for consistent, reusable connections.

## Required Values in Vault

```
{
   "secret": {
         "host": "xxxxxxxx (String Type)",
         "port": "xxxxxxxx (String Type)"
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
        "integration": "ignite",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "ignite/secret"
        },
        "action": [
            {
                "put_val": {
                    "cache_name": "test_cache",
                    "key": "key",
                    "value": "value"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "user": "test user",
        "integration": "ignite",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "ignite/server1"
        },
        "error": false,
        "action": [
            {
                "put_val": null,
            }
        ]
    }

    ```

## Functions

### `put_val`

**put_val**: This function puts a key-value pair into a specified cache.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cache_name | str | Name of the cache | yes |
    | key | str | Key to insert | yes |
    | value | str | Value to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "put_val": {
            "cache_name": "test_cache",
            "key": "key",
            "value": "value"
        }
    }
    ```

### `put_dict_val`

**put_dict_val**: This function puts a key-value pair into a specified cache, where the value is a dictionary.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cache_name | str | Name of the cache | yes |
    | key | str | Key to insert | yes |
    | value | dict | Dictionary value to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the operation was successful |

=== "JSON"

    ```json
    {
        "put_dict_val": {
            "cache_name": "test_cache",
            "key": "dict_key",
            "value": {
                "foo": "bar"
            }
        }
    }
    ```

### `get_val`

**get_val**: This function retrieves a value for a given key from a specified cache.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cache_name | str | Name of the cache | yes |
    | key | str | Key to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | any | The value associated with the key |

=== "JSON"

    ```json
    {
        "get_val": {
            "cache_name": "test_cache",
            "key": "key"
        }
    }
    ```

### `get_mul_val`

**get_mul_val**: This function retrieves multiple values for given keys from a specified cache.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cache_name | str | Name of the cache | yes |
    | keys | list | List of keys to retrieve | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of key-value pairs for the requested keys |

=== "JSON"

    ```json
    {
        "get_mul_val": {
            "cache_name": "test_cache",
            "keys": [
                "foo",
                "test_key"
            ]
        }
    }
    ```

### `cache_scan`

**cache_scan**: This function scans and retrieves all key-value pairs from a specified cache.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cache_name | str | Name of the cache | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary of all key-value pairs in the cache |

=== "JSON"

    ```json
    {
        "cache_scan": {
            "cache_name": "test_cache"
        }
    }
    ```

### `run_sql`

**run_sql**: This function executes a SQL command on the Ignite cluster.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | sql_command | str | SQL command to execute | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Result of the SQL command execution |

=== "JSON"

    ```json
    {
        "run_sql": {
            "sql_command": "DROP TABLE Test IF EXISTS"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Apache Ignite credentials in EasyTask?
Use the EasyTask vault system to securely store your Ignite connection details. Navigate to the integration configuration page and add your server details under a vault key like `ignite/server1`. Include the host and port of your Ignite cluster.

### Can I use Apache Ignite with both EasyTask Cloud and On-Premises?
Yes, Apache Ignite works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the Ignite cluster nodes are reachable from the integration server.

### How do I troubleshoot Apache Ignite connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your host and port in the vault, ensure the Ignite cluster is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
