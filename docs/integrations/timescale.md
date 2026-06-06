---
title: TimescaleDB - EasyTask Integration Guide
description: Connect TimescaleDB with EasyTask for automated time-series database operations, hypertable management, and data manipulation in scheduled workflows.
keywords:
  - timescaledb
  - easytask
  - workflow orchestration
  - automation
  - time-series database
  - scheduled database tasks
  - timescale integration
---

# TimescaleDB API

The TimescaleDB API provides a set of endpoints for managing databases, tables, and performing CRUD operations. It allows users to interact with TimescaleDB clusters programmatically.

## Why Integrate TimescaleDB with EasyTask?

TimescaleDB is a powerful time-series database built on PostgreSQL, designed for handling high-volume time-series and analytics workloads. By integrating TimescaleDB with EasyTask, you can automate database management, hypertable operations, and time-series data manipulation on a configurable schedule. EasyTask enables you to create and manage databases, perform CRUD operations on time-series data, and orchestrate data retention policies — all triggered by scheduled tasks. This integration is ideal for building IoT data pipelines, automating financial data aggregation, and scheduling analytics workflows without manual intervention.

## Required Values in Vault

```
{
    "is_credentials": {
        "userid": "test",
        "passwd": "test123"
    },
    "integrations": {
        "secret": {
           "host": "xx.x.xx.xxx",
           "password": "*******",
           "port": "xxxx",
           "user": "xxxxx"
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
        "integration": "timescaledb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "timescaledb/secret"
        },
        "action": [
            {
                "list_database_name": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "timescaledb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
                    "vault_path_key": "timescaledb/secret"
        },
        "error": false,
        "action": [
           {"list_database_name": ["postgres", "timescaledb"]}
        ]
    }

    ```

## Functions

### `list_database_name`

**list_database_name**: This function retrieves a list of all database names in the TimescaleDB cluster.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all database names |

=== "JSON"

    ```json
    {
        "list_database_name": {}
    }
    ```

### `get_current_database`

**get_current_database**: This function retrieves the name of the currently connected database.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Name of the current database |

=== "JSON"

    ```json
    {
        "get_current_database": {}
    }
    ```

### `create_table`

**create_table**: This function creates a new table in the specified TimescaleDB database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to be created | yes |
    | columns | dict | Dictionary of column names and their data types | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the table is created successfully |

=== "JSON"

    ```json
    {
        "create_table": {
            "table_name": "test_table",
            "columns": {
                "id": "INT",
                "name": "VARCHAR",
                "age": "INT"
            }
        }
    }
    ```

### `insert_table`

**insert_table**: This function inserts a new row into the specified table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to insert data into | yes |
    | data | dict | Dictionary of column names and their values | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the data is inserted successfully |

=== "JSON"

    ```json
    {
        "insert_table": {
            "table_name": "test_table",
            "data": {
                "id": "1",
                "name": "John",
                "age": "25"
            }
        }
    }
    ```

### `fetch_table`

**fetch_table**: This function retrieves all rows from the specified table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to fetch data from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries, each representing a row in the table |

=== "JSON"

    ```json
    {
        "fetch_table": {
            "table_name": "test_table"
        }
    }
    ```

### `update_table`

**update_table**: This function updates an existing row in the specified table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to update data in | yes |
    | data | dict | Dictionary of column names and their new values | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the data is updated successfully |

=== "JSON"

    ```json
    {
        "update_table": {
            "table_name": "test_table",
            "data": {
                "id": "2",
                "name": "pqr"
            }
        }
    }
    ```

### `drop_table`

**drop_table**: This function drops (deletes) the specified table from the database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to be dropped | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the table is dropped successfully |

=== "JSON"

    ```json
    {
        "drop_table": {
            "table_name": "test_table"
        }
    }
    ```

### `close_connection`

**close_connection**: This function closes the active database connection.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the connection is closed successfully |

=== "JSON"

    ```json
    {
        "close_connection": {}
    }
    ```

## FAQ

### What TimescaleDB operations does EasyTask support?

EasyTask supports a full range of TimescaleDB operations including database listing and management, table creation, data insertion and querying, connection management, and CRUD operations. You can automate the complete lifecycle of time-series data management through scheduled tasks.

### How is TimescaleDB different from PostgreSQL in EasyTask?

TimescaleDB is built on PostgreSQL but extends it with time-series optimized features like hypertables, continuous aggregates, and data retention policies. The EasyTask TimescaleDB integration leverages these capabilities for scheduling time-series specific operations while maintaining full PostgreSQL compatibility.

### Can I automate data retention and cleanup in TimescaleDB?

Yes. You can use EasyTask's scheduling capabilities to automate data retention policies, drop old partitions, and manage hypertable compression on a regular schedule. This ensures your time-series database remains performant without manual maintenance.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
