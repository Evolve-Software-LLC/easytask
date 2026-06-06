---
title: MSSQL - EasyTask Integration Guide
description: Connect Microsoft SQL Server with EasyTask for automated database operations. Step-by-step setup, configuration, and best practices for MSSQL integration.
keywords:
  - mssql
  - microsoft sql server
  - easytask
  - workflow orchestration
  - automation
  - database integration
---

# MSSQL API

The MSSQL API provides a set of operations for interacting with Microsoft SQL Server databases, allowing users to create tables, insert data, fetch records, update data, delete records, and drop tables.

## Why Integrate MSSQL with EasyTask?

Integrating Microsoft SQL Server with EasyTask enables you to automate database operations within your enterprise workflows. This integration allows you to:

- **Automate Full CRUD Operations**: Programmatically create tables, insert, fetch, update, and delete records without manual SQL execution.
- **Streamline Database Maintenance**: Schedule table creation, data migrations, and cleanup tasks as part of automated workflow pipelines.
- **Secure Credential Management**: Store MSSQL server addresses, usernames, and passwords safely in the EasyTask vault with role-based access control.

## Required Values in Vault

```
{
   "secret": {
      "database": "xyz_database",
      "mssql_password": "********",
      "mssql_server": "xxx.xxx.xxx.xxx",
      "mssql_user": "abc"
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
        "integration": "mssql",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "mssql/secret"
        },
        "action": [
            {
                "create_table": {
                    "cols": {
                        "s_id": "int not null",
                        "f_name": "varchar(50)",
                        "l_name": "varchar(50)"
                    },
                    "table": "test_table_new"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "user": "test user",
        "user": "test user",
        "integration": "mssql"
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "mssql/server1"
        },
        "error": false,
        "action": [
            {
                "create_table": null
            }
        ]
    }

    ```

## Functions

### `create_table`

**create_table**: This function creates a new table in the MSSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | cols | dict | Dictionary of column names and their data types | yes |
    | table | str | Name of the table to be created | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the table was created successfully |

=== "JSON"

    ```json
    {
        "create_table": {
            "cols": {
                "s_id": "int not null",
                "f_name": "varchar(50)",
                "l_name": "varchar(50)"
            },
            "table": "test_table_new"
        }
    }
    ```

### `insert_table`

**insert_table**: This function inserts rows into a table in the MSSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table | str | Name of the table to insert into | yes |
    | rows | list | List of lists, each inner list representing a row to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the rows were inserted successfully |

=== "JSON"

    ```json
    {
        "insert_table": {
            "table": "test_table_new",
            "rows": [
                [1, "alan", "turing"],
                [2, "nikola", "tesla"],
                [3, "alan", "walker"]
            ]
        }
    }
    ```

### `fetch_table`

**fetch_table**: This function fetches rows from a table in the MSSQL database based on specified conditions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table | str | Name of the table to fetch from | yes |
    | cols | dict | Dictionary of column names and values to filter by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries, each representing a row that matches the conditions |

=== "JSON"

    ```json
    {
        "fetch_table": {
            "table": "test_table_new",
            "cols": {
                "f_name": "alan"
            }
        }
    }
    ```

### `update_table`

**update_table**: This function updates rows in a table in the MSSQL database based on specified conditions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table | str | Name of the table to update | yes |
    | setcol | dict | Dictionary of column names and values to update | yes |
    | wherecol | dict | Dictionary of column names and values to filter by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the update was successful |

=== "JSON"

    ```json
    {
        "update_table": {
            "table": "test_table_new",
            "setcol": {
                "f_name": "nicola"
            },
            "wherecol": {
                "f_name": "nikola"
            }
        }
    }
    ```

### `delete_table`

**delete_table**: This function deletes rows from a table in the MSSQL database based on specified conditions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table | str | Name of the table to delete from | yes |
    | wherecol | dict | Dictionary of column names and values to filter by | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the deletion was successful |

=== "JSON"

    ```json
    {
        "delete_table": {
            "table": "test_table_new",
            "wherecol": {
                "f_name": "nikola"
            }
        }
    }
    ```

### `drop_table`

**drop_table**: This function drops (deletes) a table from the MSSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | table | str | Name of the table to drop | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the table was dropped successfully |

=== "JSON"

    ```json
    {
        "drop_table": {
            "table": "test_table_new"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure MSSQL credentials in EasyTask?
Use the EasyTask vault system to securely store your MSSQL connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `mssql/server1`. Include the MSSQL server address, database name, username, and password.

### Can I use MSSQL with both EasyTask Cloud and On-Premises?
Yes, MSSQL works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the SQL Server instance is reachable from the integration server.

### How do I troubleshoot MSSQL connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials in the vault, ensure the MSSQL server is accessible from the integration server, and test connectivity using the built-in connection test feature. Confirm that the database name and user permissions are correct.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
