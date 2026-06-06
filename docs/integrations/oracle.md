---
title: Oracle Database - EasyTask Integration Guide
description: Connect Oracle Database with EasyTask for automated database operations. Step-by-step setup, configuration, and best practices for Oracle integration.
keywords:
  - oracle
  - oracle database
  - easytask
  - workflow orchestration
  - automation
  - database integration
---

# Oracle API

The Oracle API provides a set of operations for interacting with Oracle databases, allowing users to create tables, insert data, update records, delete data, and perform various queries.

## Why Integrate Oracle Database with EasyTask?

Integrating Oracle Database with EasyTask enables you to automate enterprise-grade database operations within your workflows. This integration allows you to:

- **Automate Full Database Lifecycle**: Programmatically create, populate, query, update, and drop tables as part of automated data pipeline workflows.
- **Leverage Advanced SQL Analytics**: Use built-in aggregate functions (min, max, avg, sum, count) and sorted queries directly in your automated workflows.
- **Secure Connection Management**: Store Oracle DSN, usernames, and passwords in the EasyTask vault for centralized, secure credential management.

## Required Values in Vault

```
{
   "secret": {
      "database": "xyz_database",
      "oracle_dsn": "xxx.xxx.xxx.xxx",
      "oracle_password": "******",
      "oracle_user": "xyz"
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
        "integration": "oracle",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "oracle/secret"
        },
        "action": [
            {
                "create_table": {
                    "table_name": "test_table",
                    "cols": {
                        "sno": "NUMBER",
                        "fname": "VARCHAR2(30)",
                        "lname": "VARCHAR2(30)",
                        "sal": "NUMBER"
                    }
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    {
    "integration": "oracle",
    "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
    "init": {
        "vault_path_key": "oracle/server1"
    },
    "error":false,
    "action": [
        {
            "create_table": null
        }
    ]
    }
    ```

## Functions

### `create_table`

**create_table**: This function creates a new table in the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to create | yes |
    | cols | dict | Dictionary of column names and their data types | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the table was created successfully |

=== "JSON"

    ```json
    {
        "create_table": {
            "table_name": "test_table",
            "cols": {
                "sno": "NUMBER",
                "fname": "VARCHAR2(30)",
                "lname": "VARCHAR2(30)",
                "sal": "NUMBER"
            }
        }
    }
    ```

### `construct_sql`

**construct_sql**: This function constructs a SQL query based on provided columns and qualifiers.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cols | dict | Dictionary of column names and values | yes |
    | qualifier | str | SQL qualifier (e.g., "AND", "OR") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Constructed SQL query |

=== "JSON"

    ```json
    {
        "construct_sql": {
            "cols": {},
            "qualifier": ""
        }
    }
    ```

### `insert_into_table`

**insert_into_table**: This function inserts records into a table in the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to insert into | yes |
    | cols | list | List of column names | yes |
    | records | list | List of lists, each inner list representing a record to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the records were inserted successfully |

=== "JSON"

    ```json
    {
        "insert_into_table": {
            "table_name": "test_table",
            "cols": ["sno", "fname", "lname", "sal"],
            "records": [
                [1, "John", "Mathew", 3000],
                [2, "Sheldon", "Cooper", 4000],
                [3, "Howard", "Wolowitz", 3000]
            ]
        }
    }
    ```

### `update_table`

**update_table**: This function updates records in a table in the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to update | yes |
    | setcol | dict | Dictionary of columns and values to set | yes |
    | cols | dict | Dictionary of columns and values to filter by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the update was successful |

=== "JSON"

    ```json
    {
        "update_table": {
            "table_name": "test_table",
            "setcol": {
                "lname": "Parker"
            },
            "cols": {
                "lname": "Mathew"
            }
        }
    }
    ```

### `delete_table_with_filter`

**delete_table_with_filter**: This function deletes records from a table in the Oracle database based on specified conditions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to delete from | yes |
    | cols | dict | Dictionary of columns and values to filter by | yes |
    | qualifier | str | SQL qualifier (e.g., "AND", "OR") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the deletion was successful |

=== "JSON"

    ```json
    {
        "delete_table_with_filter": {
            "table_name": "test_table",
            "cols": {
                "fname": "Parker"
            },
            "qualifier": "AND"
        }
    }
    ```

### `delete_table`

**delete_table**: This function deletes all records from a table in the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to delete from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the deletion was successful |

=== "JSON"

    ```json
    {
        "delete_table": {
            "table_name": "test_table"
        }
    }
    ```

### `drop_table`

**drop_table**: This function drops (deletes) a table from the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to drop | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the table was dropped successfully |

=== "JSON"

    ```json
    {
        "drop_table": {
            "table_name": "test_table"
        }
    }
    ```

### `fetch_table`

**fetch_table**: This function retrieves all records from a table in the Oracle database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table to fetch from | yes |

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

### `get_min`

**get_min**: This function retrieves the minimum value of a specified column in a table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | column | str | Name of the column to get the minimum value from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | number | Minimum value of the specified column |

=== "JSON"

    ```json
    {
        "get_min": {
            "table_name": "test_table",
            "column": "sal"
        }
    }
    ```

### `get_max`

**get_max**: This function retrieves the maximum value of a specified column in a table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | column | str | Name of the column to get the maximum value from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | number | Maximum value of the specified column |

=== "JSON"

    ```json
    {
        "get_max": {
            "table_name": "test_table",
            "column": "sal"
        }
    }
    ```

### `get_avg`

**get_avg**: This function retrieves the average value of a specified column in a table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | column | str | Name of the column to get the average value from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | number | Average value of the specified column |

=== "JSON"

    ```json
    {
        "get_avg": {
            "table_name": "test_table",
            "column": "sal"
        }
    }
    ```

### `get_sum`

**get_sum**: This function retrieves the sum of values in a specified column in a table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | column | str | Name of the column to get the sum from | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | number | Sum of values in the specified column |

=== "JSON"

    ```json
    {
        "get_sum": {
            "table_name": "test_table",
            "column": "sal"
        }
    }
    ```

### `get_count`

**get_count**: This function retrieves the count of rows in a table, optionally for a specific column.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | column | str | Name of the column to count (optional) | no |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of rows or non-null values in the specified column |

=== "JSON"

    ```json
    {
        "get_count": {
            "table_name": "test_table",
            "column": "sal"
        }
    }
    ```

### `sort_rows`

**sort_rows**: This function retrieves sorted rows from a table based on specified columns and order.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table_name | str | Name of the table | yes |
    | order_by_col | str | Column to sort by | yes |
    | cols | list | List of columns to retrieve | yes |
    | qualifier | str | Sort order qualifier (e.g., "ASC", "DESC") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries, each representing a sorted row |

=== "JSON"

    ```json
    {
        "sort_rows": {
            "table_name": "test_table",
            "order_by_col": "sal",
            "cols": ["sno", "fname"],
            "qualifier": "DESC"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Oracle credentials in EasyTask?
Use the EasyTask vault system to securely store your Oracle connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `oracle/server1`. Include the DSN, database name, username, and password.

### Can I use Oracle with both EasyTask Cloud and On-Premises?
Yes, Oracle Database works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the Oracle server is reachable from the integration server.

### How do I troubleshoot Oracle connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials in the vault, ensure the Oracle server is accessible from the integration server, and test connectivity using the built-in connection test feature. Confirm the DSN string and database name are correct.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
