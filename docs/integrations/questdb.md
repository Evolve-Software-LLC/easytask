---
title: QuestDB - EasyTask Integration Guide
description: Connect QuestDB with EasyTask for automated time-series database operations. Step-by-step setup, configuration, and best practices for QuestDB integration.
keywords:
  - questdb
  - time-series database
  - easytask
  - workflow orchestration
  - automation
  - database integration
---

# QuestDB

QuestDB is a high-performance, open-source time-series database designed for real-time analytics and handling large volumes of time-stamped data. It offers SQL compatibility, supports high-throughput ingestion, and is optimized for fast queries, making it ideal for use cases like IoT, financial systems, and monitoring.

## Why Integrate QuestDB with EasyTask?

Integrating QuestDB with EasyTask enables you to automate time-series data operations within your workflows. This integration allows you to:

- **Automate Time-Series Data Ingestion**: Programmatically insert data via PostgreSQL wire protocol or CSV imports as part of your real-time data pipelines.
- **Streamline Query and Export Workflows**: Execute SQL queries and export results to CSV files automatically for reporting and analysis.
- **Manage Database Lifecycle**: Create, update, and drop tables, then close connections cleanly — all orchestrated through EasyTask workflows.

## Integration Server Vault details

### Required secrets in Vault

=== "Table"

    | Key | Description |
    |-----|-------------|
    | port | The port number for the database connection |
    | database | The name of the database |
    | host | The hostname or IP address of the database server |
    | password | The password for authentication |
    | user | The username for authentication |

=== "JSON"

    ```json
    {
      "secret": {
        "port": "xxxx",
        "database": "xyz_database",
        "host": "xxx.xxx.xxx.xxx",
        "password": "*******",
        "user": "xyz"
      }
    }
    ```

## Example cURL Commands

### Sample Usage of QuestDB 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d'
      {
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [
            {
              "integration": "questdb",
              "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
              "init": {
              "vault_path_key": "questdbv1/secret"
              },
              "action": [
                  {
                    "insert_table_postgres": {
                        "table_name": "test",
                        "data": {
                        "id": "1",
                        "name": "xyz"
                        }
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
         "insert_table_postgres": "Data inserted successfully"
        }
    }
    ```

## Functions

### `create_table`

**Create a QuestDB table**:

This function creates a new table in QuestDB with specified columns and their types.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be created | Yes |
    | columns | object | Dictionary of column names and their types | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_table action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "create_table": {
                "table_name": "test",
                "columns": {
                  "id": "INT",
                  "name": "STRING"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `insert_table_postgres`

**Inserting into QuestDB table**:

This function inserts a record into a QuestDB table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to insert data into | Yes |
    | data | object | Dictionary of column names and their values | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the insert_table_postgres action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "insert_table_postgres": {
                "table_name": "test",
                "data": {
                  "id": "1",
                  "name": "xyz"
                }
              }
            }
          ]
        }
      ]
    }'
    ```

### `fetch_table_postgres`

**Fetching data with filters from QuestDB table**:

This function retrieves data from a QuestDB table based on specified filters.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to fetch data from | Yes |
    | conditions | string | Column names and search filters for WHERE clause | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the fetch_table_postgres action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "fetch_table_postgres": {
                "table_name": "test"
              }
            }
          ]
        }
      ]
    }
    ```

### `update_table_postgres`

**Updating data in QuestDB table**:

This function updates data in a QuestDB table based on specified conditions.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to update | Yes |
    | data | object | Dictionary of column names and their updated values | Yes |
    | conditions | string | Column names and search filters for WHERE clause | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_table_postgres action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "update_table_postgres": {
                "table_name": "test",
                "data": {
                  "id": "2",
                  "name": "'pqr'"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `drop_table_postgres`

**Dropping QuestDB table**:

This function removes a table from QuestDB.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to be dropped | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the drop_table_postgres action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "drop_table_postgres": {
                "table_name": "test"
              }
            }
          ]
        }
      ]
    }
    ```

### `insert_table_csv`

**Insert data from a CSV Table in QuestDB**:

This function inserts data from a CSV file into a QuestDB table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | table_name | string | Name of the table to insert data into | Yes |
    | csv_file_path | string | File path of the CSV | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the insert_table_csv action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "insert_table_csv": {
                "table_name": "csv_table",
                "csv_file_path": "quest_test.csv"
              }
            }
          ]
        }
      ]
    }
    ```

### `query_questdb_to_csv`

**Query QuestDB to CSV**:

This function executes a query on QuestDB via the HTTP API and stores the results in a CSV file.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | query | string | Query to execute | Yes |
    | csv_file_path | string | Path of the CSV file to store results | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the query_questdb_to_csv action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "query_questdb_to_csv": {
                "query": "select * from test_table",
                "csv_file_path": "quest_results.csv"
              }
            }
          ]
        }
      ]
    }
    ```

### `close_connection`

**Close the connection**:

This function closes the connection to QuestDB.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (questdb) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the close_connection action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "questdb",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "questdbv1/secret"
          },
          "action": [
            {
              "close_connection": {}
            }
          ]
        }
      ]
    }
    ```

---

## Frequently Asked Questions

### How do I configure QuestDB credentials in EasyTask?
Use the EasyTask vault system to securely store your QuestDB connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `questdbv1/secret`. Include the host, port, database name, username, and password.

### Can I use QuestDB with both EasyTask Cloud and On-Premises?
Yes, QuestDB works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the QuestDB server is reachable from the integration server.

### How do I troubleshoot QuestDB connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials in the vault, ensure the QuestDB server is accessible from the integration server, and test connectivity using the built-in connection test feature. Confirm that the PostgreSQL wire protocol port is open and accepting connections.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
