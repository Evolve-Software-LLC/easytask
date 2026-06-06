---
title: CockroachDB - EasyTask Integration Guide
description: Connect CockroachDB with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for distributed SQL database operations.
keywords:
  - cockroachdb
  - easytask
  - workflow orchestration
  - automation
  - distributed sql
  - database
---

# CockroachDB API

The CockroachDB API provides a set of endpoints for managing databases, tables, and performing CRUD operations. It allows users to interact with CockroachDB clusters programmatically.

## Why Integrate CockroachDB with EasyTask?

Integrating CockroachDB with EasyTask enables you to automate distributed SQL database operations at scale. This integration allows you to:

- **Automate Database Operations**: Create tables, insert records, update data, and fetch results programmatically as part of your automated EasyTask workflows.
- **Scale Distributed Workloads**: Leverage CockroachDB's horizontal scalability within your EasyTask orchestration to handle growing data requirements seamlessly.
- **Ensure Data Consistency**: Perform reliable CRUD operations on a strongly consistent distributed database, ensuring data integrity across your automated pipelines.

## Required Values in Vault

```
{

        "secret": {
            "url": "xxxxxxxx"
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
        "integration": "cockroachdb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "cockroachdb/secret"
        },
        "action": [
            {
                "create_table": {
                    "table_name": "example_table",
                    "columns": {
                        "id": "INT",
                        "name": "TEXT"
                    }
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "cockroachdb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
                    "vault_path_key": "cockroachdb/secret"
        },
        "error": false,
        "action": [
            {
                "create_table": "Table example_table created successfully"
                }
        ]
    }

    ```

## Functions

### `create_table`

**create_table**: This function creates a new table in the specified CockroachDB database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to be created | yes |
    | columns | dict | Dictionary of column names and their data types | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | None | Returns null if the table is created successfully |

=== "JSON"

    ```json
    {
        "create_table": {
            "table_name": "example_table",
            "columns": {
                "id": "INT",
                "name": "TEXT"
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
    | values | dict | Dictionary of column names and their values | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | None | Returns null if the data is inserted successfully |

=== "JSON"

    ```json
    {
        "insert_table": {
            "table_name": "example_table",
            "values": {
                "id": "1",
                "name": "John"
            }
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
    | response | None | Returns null if the data is updated successfully |

=== "JSON"

    ```json
    {
        "update_table": {
            "table_name": "example_table",
            "data": {
                "id": "1",
                "name": "Johnnny"
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
            "table_name": "example_table"
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
    | response | None | Returns null if the table is dropped successfully |

=== "JSON"

    ```json
    {
        "drop_table": {
            "table_name": "example_table"
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
    | response | None | Returns null if the connection is closed successfully |

=== "JSON"

    ```json
    {
        "close_connection": {}
    }
    ```

---

## Frequently Asked Questions

### How do I configure CockroachDB credentials in EasyTask?
Use the EasyTask vault system to securely store your CockroachDB connection URL. Navigate to the integration configuration page and add your database URL under a vault key like `cockroachdb/secret`.

### Can I use CockroachDB with both EasyTask Cloud and On-Premises?
Yes, CockroachDB works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot CockroachDB connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your database URL in the vault, ensure the CockroachDB cluster is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
