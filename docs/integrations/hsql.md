---
title: HSQL - EasyTask Integration Guide
description: Connect HSQL (HyperSQL) with EasyTask for automated database operations. Step-by-step setup, configuration, and best practices for HSQLDB integration.
keywords:
  - hsql
  - hsqldb
  - easytask
  - workflow orchestration
  - automation
  - database integration
---

# HSQL

HSQL (HyperSQL) is a lightweight, high-performance relational database management system written in Java. It supports a range of SQL standards and offers in-memory and disk-based tables. HSQL is commonly used for embedded database applications, testing, and teaching, known for its speed and small footprint.

## Why Integrate HSQL with EasyTask?

Integrating HSQL (HyperSQL) with EasyTask enables you to automate database operations directly within your workflows. This integration allows you to:

- **Streamline Database Management**: Automate table creation, data insertion, updates, and deletions without manual intervention.
- **Accelerate Testing Pipelines**: Use HSQLDB's lightweight in-memory capabilities for rapid test data setup and teardown in automated workflows.
- **Centralize Credentials Securely**: Store and manage HSQLDB connection details in the EasyTask vault system for secure, role-based access.

## Integration Server Vault details

### Required Secrets in Vault

=== "Table"

    | Key | Description |
    |-----|-------------|
    | hsqldb_host | The hostname or IP address of the HSQLDB server |
    | hsqldb_password | The password for connecting to the HSQLDB server |
    | hsqldb_port | The port number on which the HSQLDB server is running |
    | hsqldb_username | The username for connecting to the HSQLDB server |
    | jar_path | The file system path to the HSQLDB JAR file |

=== "JSON"

    ```json
    {
      "secret": {
        "hsqldb_host": "xxx.xxx.xxx.xxx",
        "hsqldb_password": "xxxxxxxxx",
        "hsqldb_port": "xxxxx",
        "hsqldb_username": "xxxxx",
        "jar_path": "/path/to/jarfile/hsqldb.jar"
      }
    }
    ```

### HSQL Integration Instance Creation

=== "Table"

    | Key | Description |
    |-----|-------------|
    | is_credentials | Object containing user credentials |
    | integrations | Array of integration objects |
    | integration | Type of integration (hsqldb in this case) |
    | uuid | Unique identifier for the integration instance |
    | init | Initialization parameters |
    | vault_path_key | Path to the vault containing HSQLDB credentials |
    | action | Array of actions to be performed (empty in this example) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "hsqldb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "hsql/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of HSQL 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [
            {
                "integration": "hsqldb",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "hsql/server1"
                },
                "action": [
                    {
                        "create_table": {
                            "cols": {
                                "CUST_ID": "INTEGER not null primary key",
                                "NAME": "VARCHAR(50) not null",
                                "YEAR": "INTEGER"
                            },
                            "table": "test2"
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
        "data": {
            "connect": null
        }
    }
    ```

##  Function of HSQL

###  `create_table`

**Create a HSQL table** :

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | CUST_ID | INTEGER not null primary key | Unique customer identifier | Yes |
    | NAME | VARCHAR(50) not null | Customer's full name | Yes |
    | YEAR | INTEGER | Relevant year (e.g., join year) | No |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (e.g., hsqldb) |
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
            "integration": "hsqldb",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "hsql/server1"
            },
            "action": [
                {
                    "create_table": {
                        "cols": {
                            "CUST_ID": "INTEGER not null primary key",
                            "NAME": "VARCHAR(50) not null",
                            "YEAR": "INTEGER"
                        },
                        "table": "test2"
                    }
                }
            ]
        }
    ]
    }

    ```

###  `insert_table`

**Inserting into a HSQL table** :
The Insert Data function allows users to add new records to an existing table in the HSQLDB database. It takes a table name and a list of rows to be inserted, and returns the status of the operation.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table | string | Name of the table to insert data into | Yes |
    | rows | array of arrays | 2D list containing the records to be inserted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (e.g., hsqldb) |
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
            "integration": "hsqldb",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "hsql/server1"
            },
            "action": [
                {
                    "insert_table": {
                        "table": "test2",
                        "rows": [
                            [
                                1,
                                "Rachel",
                                2005
                            ],
                            [
                                2,
                                "Monica",
                                2006
                            ],
                            [
                                3,
                                "Chandler",
                                2007
                            ]
                        ]
                    }
                }
            ]
        }
    ]
    }
    ```

###  `fetch_table`

**HSQLDB Fetch Data** :
The Fetch Data function retrieves data from a specified table in the HSQLDB database based on given conditions. It takes a table name and filter conditions, and returns the matching records along with the operation status.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table | string | Name of the table to fetch data from | Yes |
    | where | object | Conditions for filtering the data | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (e.g., hsqldb) |
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
            "integration": "hsqldb",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "hsql/server1"
            },
            "action": [
                {
                    "fetch_table": {
                        "table": "test2",
                        "where": {
                            "year": "2005"
                        }
                    }
                }
            ]
        }
    ]
    }
    ```

###  `update_table`

**HSQLDB Update Data** :
The Update Data function allows users to modify existing records in a specified table in the HSQLDB database. It takes a table name, the columns and values to be updated, and the conditions for selecting which rows to update. The function returns the status of the operation and any relevant action results.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table | string | Name of the table to update data in | Yes |
    | set_cols | object | Columns and values to be updated | Yes |
    | where_cols | object | Conditions for filtering the rows to update | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (hsqldb) |
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
            "integration": "hsqldb",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "hsql/server1"
            },
            "action": [
                {
                    "update_table": {
                        "table": "test2",
                        "set_cols": {
                            "year": "2005"
                        },
                        "where_cols": {
                            "year": "2022"
                        }
                    }
                }
            ]
        }
    ]
    }
    ```

###  `delete_table`

**Deleting data in a HSQL table** :
The Delete function removes specific records from an HSQLDB table based on provided conditions. It requires a table name and filter criteria, equivalent to a SQL DELETE statement. The function returns the operation's status, indicating success or any errors encountered.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table | string | Name of the table to delete data from | Yes |
    | where_cols | object | Conditions for filtering the rows to delete | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (hsqldb) |
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
            "integration": "hsqldb",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "hsql/server1"
            },
            "action": [
                {
                    "delete_table": {
                        "table": "test2",
                        "where_cols": {
                            "year": "2022"
                        }
                    }
                }
            ]
        }
    ]
    }
    ```

###  `drop_table`

**Dropping a HSQL table** :
The Drop Table function removes an entire table from the HSQLDB database. It requires only the table name and permanently deletes the table structure and all its data.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table | string | Name of the table to be dropped | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (hsqldb) |
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
                "integration": "hsqldb",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "hsql/server1"
                },
                "action": [
                    {
                        "drop_table": {
                            "table": "test2"
                        }
                    }
                ]
            }
        ]
    }
    ```
