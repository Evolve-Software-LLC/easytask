---
title: SQLite - EasyTask Integration Guide
description: Connect SQLite with EasyTask for automated database operations, table management, and data manipulation in scheduled workflows.
keywords:
  - sqlite
  - easytask
  - workflow orchestration
  - automation
  - local database
  - scheduled database tasks
  - sqlite integration
---

# SQLite Integration

SQLite is a lightweight, serverless, self-contained SQL database engine that is the most widely deployed database in the world. Unlike client-server databases, SQLite reads and writes directly to ordinary disk files, making it ideal for embedded applications, prototyping, testing, and lightweight data storage. A complete SQLite database with tables, indexes, and data is stored in a single cross-platform disk file.

## Why Integrate SQLite with EasyTask?

SQLite is a zero-configuration, file-based relational database perfect for lightweight automation workflows. By integrating SQLite with EasyTask, you can automate table creation, data insertion, querying, and schema management on a configurable schedule — all without needing a separate database server. This integration is ideal for building local data pipelines, automating test fixtures, managing configuration stores, and scheduling periodic data aggregation tasks. With EasyTask's vault-based credential management, your SQLite file paths and access settings remain secure while enabling hands-free database operations.

## Integration Server Vault details

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "database": "/path/to/localdb.sqlite",
        "host": "localhost",
        "password": "",
        "user": ""
      }
    }
    ```

### SQLite JSON Format

An SQLite instance can be created as below by passing the vault_path_key:

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "sqlite") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing SQLite credentials | Yes |
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
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of SQLite

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d'
    {
      "is_credentials": {
          "userid": "test",
          "passwd": "test123",
      },
      "integrations": [
          {
              "integration": "sqlite",
              "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
              "init": {
                  "vault_path_key": "sqlite/localdb"
              },
              "action": [
                  {
                      "insert_data": {
                          "table_name": "my_table1",
                          "records": [
                              [
                                  1,
                                  "jake",
                                  "forest"
                              ],
                              [
                                  2,
                                  "wave",
                                  "forest"
                              ],
                              [
                                  3,
                                  "jayant",
                                  "khanna"
                              ]
                          ]
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
          "insert_data": null
        }
    }
    ```

## Available Functions

| Function | Description |
|----------|-------------|
| `create_table` | Create a new SQLite table with specified columns and types |
| `insert_data` | Insert records into a specified SQLite table |
| `fetch_data` | Retrieve data from a SQLite table with column filters |
| `del_data` | Delete specific records from a SQLite table based on criteria |
| `del_all_data` | Remove all records from a specified SQLite table |
| `drop_table` | Remove a table entirely from the SQLite database |
| `connect_to_database` | Establish a connection to a specified SQLite database file |
| `get_current_database` | Retrieve the path of the currently connected SQLite database |

### `create_table`

**Create a SQLite table**:

This function creates a new table in SQLite with specified columns and their types.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be created | Yes |
    | cols | object | Dictionary of column names and their types | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "create_table": {
                "table_name": "my_table1",
                "cols": {
                  "sno": "INTEGER",
                  "fname": "TEXT",
                  "lname": "TEXT"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `insert_data`

**Inserting into SQLite table**:

This function inserts records into a specified SQLite table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to insert data into | Yes |
    | records | array | 2D list of records to be inserted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "insert_data": {
                "table_name": "my_table1",
                "records": [
                  [1, "jake", "forest"],
                  [2, "wave", "forest"],
                  [3, "jayant", "khanna"]
                ]
              }
            }
          ]
        }
      ]
    }
    ```

### `fetch_data`

**Fetch data with filters from SQLite table**:

This function retrieves data from a SQLite table based on specified filters.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | tb_name | string | Name of the table to fetch data from | Yes |
    | cols | object | Dictionary of column names and their filter values | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "fetch_data": {
                "tb_name": "my_table1",
                "cols": {
                  "sno": 3,
                  "fname": "jayant"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `del_data`

**Deleting data in SQLite table**:

This function deletes data from a SQLite table based on specified criteria.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to delete data from | Yes |
    | cols | object | Dictionary of column names and their filter values | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "del_data": {
                "table_name": "my_table1",
                "cols": {
                  "sno": 3,
                  "fname": "jayant"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `del_all_data`

**Delete all records in SQLite table**:

This function removes all data from a specified SQLite table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to delete all data from | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "del_all_data": {
                "table_name": "my_table1"
              }
            }
          ]
        }
      ]
    }
    ```

### `drop_table`

**Dropping SQLite table**:

This function removes a specified table from the SQLite database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be dropped | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "drop_table": {
                "table_name": "my_table3"
              }
            }
          ]
        }
      ]
    }
    ```

### `connect_to_database`

**Connect to Database**:

This function establishes a connection to a specified SQLite database file.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | db_name | string | Path to the SQLite database file to connect to | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "connect_to_database": {
                "db_name": "/path/to/my_database.sqlite"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_current_database`

**Get Current Database**:

This function retrieves the file path of the currently connected SQLite database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (sqlite) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | List of actions performed, with their results |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "sqlite",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "sqlite/localdb"
          },
          "action": [
            {
              "get_current_database": {}
            }
          ]
        }
      ]
    }
    ```

## FAQ

### Does SQLite require a separate server or installation?

No. SQLite is a serverless, file-based database engine. The entire database is stored as a single file on disk. With EasyTask, you only need to specify the file path in your vault configuration — no database server setup, configuration, or administration is required.

### What SQLite operations does EasyTask support?

EasyTask supports a comprehensive set of SQLite operations including creating and dropping tables, inserting data, fetching data with filters, deleting specific or all records, connecting to database files, and retrieving the current database path. You can automate the full lifecycle of SQLite data management through scheduled tasks.

### Can I use SQLite for production workflows with EasyTask?

SQLite is ideal for lightweight automation, prototyping, testing, and local data aggregation tasks. For high-concurrency production workloads or large-scale data processing, consider using a client-server database like PostgreSQL or MySQL. However, SQLite works perfectly for single-writer scheduled tasks, configuration stores, and embedded data pipelines.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
