---
description: PostgreSQL integration for EasyTask — automate database operations, table management, and data manipulation in scheduled workflows.
keywords:
  - PostgreSQL task scheduling
  - database automation
  - SQL workflow orchestration
  - scheduled database tasks
  - PostgreSQL integration
  - automated SQL operations
---

# PostgreSQL

PostgreSQL is a powerful, open-source relational database management system known for its advanced features and extensibility It supports SQL and JSON querying, offering robust performance, data integrity, and scalability. Favored for complex applications, PostgreSQL is widely used for web services, data warehousing, and scientific computing.

## Why Integrate PostgreSQL with EasyTask?

PostgreSQL is a powerful open-source relational database trusted by organizations worldwide for its reliability, advanced feature set, and extensibility. By integrating PostgreSQL with EasyTask, you can leverage scheduled tasks to automate a wide range of database operations. EasyTask enables you to create tables, insert and query data, manage databases, and execute complex SQL operations — all triggered on configurable schedules. This integration is ideal for building ETL workflows, automating reporting pipelines, and scheduling routine database maintenance tasks without manual intervention.

## Integration Server Vault details

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "database": "xyz_database",
        "host": "xxx.xxx.xxx.xxx",
        "password": "*******",
        "user": "xyz"
      }
    }
    ```

### PostgreSQL JSON Format

An PostgreSQL instance can be created as below by passing the vault_path_key:

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "postgresql") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing PostgreSQL credentials | Yes |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of PostgreSQL 

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
              "integration": "postgresql",
              "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
              "init": {
                  "vault_path_key": "postgresql/server1"
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

## Functions

### `create_table`

**Create a PostgreSQL table**:

This function creates a new table in PostgreSQL with specified columns and their types.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be created | Yes |
    | cols | object | Dictionary of column names and their types | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "create_table": {
                "table_name": "my_table1",
                "cols": {
                  "sno": "int",
                  "fname": "varchar(50)",
                  "lname": "varchar(50)"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `insert_data`

**Inserting into PostgreSQL table**:

This function inserts records into a specified PostgreSQL table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to insert data into | Yes |
    | records | array | 2D list of records to be inserted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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
    }'
    ```

### `fetch_data`

**Fetch data with filters from PostgreSQL table**:

This function retrieves data from a PostgreSQL table based on specified filters.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | tb_name | string | Name of the table to fetch data from | Yes |
    | cols | object | Dictionary of column names and their filter values | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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
    }'
    ```

### `del_data`

**Deleting data in PostgreSQL table**:

This function deletes data from a PostgreSQL table based on specified criteria.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to delete data from | Yes |
    | cols | object | Dictionary of column names and their filter values | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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

**Delete all records in PostgreSQL table**:

This function removes all data from a specified PostgreSQL table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to delete all data from | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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

**Dropping PostgreSQL table**:

This function removes a specified table from the PostgreSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be dropped | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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

### `create_database`

**Create Database**:

This function creates a new PostgreSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | db_name | string | Name of the database to be created | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "create_database": {
                "db_name": "database"
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_database`

**Delete Database**:

This function deletes a specified PostgreSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | db_name | string | Name of the database to be deleted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "delete_database": {
                "db_name": "database"
              }
            }
          ]
        }
      ]
    }
    ```

### `connect_to_database`

**Connect to Database**:

This function establishes a connection to a specified PostgreSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | db_name | string | Name of the database to connect to | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "connect_to_database": {
                "db_name": "database"
              }
            }
          ]
        }
      ]
    }
    ```

### `rollback`

**Rollback**:

This function performs a rollback operation on the current PostgreSQL transaction.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "rollback": {}
            }
          ]
        }
      ]
    }
    ```

### `get_current_database`

**Get Current Database**:

This function retrieves the name of the currently connected PostgreSQL database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
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

### `get_all_databases`

**Get All Databases**:

This function retrieves information about all databases in the PostgreSQL instance.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "get_all_databases": {}
            }
          ]
        }
      ]
    }
    ```

### `construct_where_clause`

**Construct Where Clause**:

This function constructs a WHERE clause for SQL queries based on provided columns and qualifiers.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | cols | object | Dictionary of column names and their values | Yes |
    | qualifier | string | Additional qualifier for the WHERE clause | No |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (postgresql) |
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
          "integration": "postgresql",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "postgresql/server1"
          },
          "action": [
            {
              "construct_where_clause": {
                "cols": {
                  "hello": "world"
                },
                "qualifier": "hello world"
              }
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What PostgreSQL operations does EasyTask support?

EasyTask supports a comprehensive set of PostgreSQL operations including creating and dropping tables, inserting data, fetching data with filters, deleting specific or all records, creating and deleting databases, connecting to databases, performing rollbacks, and constructing WHERE clauses for complex queries.

### How do I automate SQL operations with scheduled tasks?

Configure your PostgreSQL integration in EasyTask by providing your vault credentials, then define actions (such as `create_table`, `insert_data`, `fetch_data`, etc.) within a scheduled task. EasyTask will execute these operations automatically at the specified intervals, enabling hands-free database automation.

### Can I create and manage databases with EasyTask?

Yes. EasyTask provides dedicated functions for database management, including `create_database`, `delete_database`, `connect_to_database`, `get_current_database`, and `get_all_databases`. You can fully automate database lifecycle management through scheduled workflows.

## Next Steps

- [Introduction to Integrations](integrations_intro.md)
- [MySQL Integration](mysql.md)
- [MongoDB Integration](mongodb.md)
