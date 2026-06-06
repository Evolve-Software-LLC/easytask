---
title: CouchDB - EasyTask Integration Guide
description: Connect CouchDB with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for NoSQL document database operations.
keywords:
  - couchdb
  - easytask
  - workflow orchestration
  - automation
  - nosql
  - document database
---

# CouchDB API

The CouchDB API provides a set of endpoints for managing databases, documents, and performing CRUD operations. It allows users to interact with CouchDB clusters programmatically.

## Why Integrate CouchDB with EasyTask?

Integrating CouchDB with EasyTask enables you to automate NoSQL document database operations with ease. This integration allows you to:

- **Automate Document Management**: Create databases, insert documents in bulk, update records, and query data programmatically as part of your EasyTask workflows.
- **Flexible Query and Search**: Use Mango queries with selectors to find, filter, and transform documents automatically, enabling sophisticated data processing pipelines.
- **Scalable Data Operations**: Perform bulk inserts, batch updates, and mass deletions efficiently through EasyTask orchestration, handling large datasets without manual effort.

## Required Values in Vault
```
{

        "secret": {
           "couch_host": "xx.x.xx.xxx",
           "couch_password": "*******",
           "couch_port": "xxxx",
           "couch_user": "xxxxx"

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
        "integration": "couchdb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "couchdb/secret"
        },
        "action": [
            {
                "create_database": {
                    "database": "couch2"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "couchdb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
                "vault_path_key": "couch/secret"
        },
        "error": false,
        "action": [
            { "create_database": "Successfully created Database" }
        ]
    }

    ```

## Functions

### `create_database`

**create_database**: This function creates a new database in CouchDB.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | database | str | Name of the database to be created | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the database is created successfully |

=== "JSON"

    ```json
    {
        "create_database": {
            "database": "couch2"
        }
    }
    ```

### `create_collection`

**create_collection**: This function creates a new document in the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | doc_id | str | ID of the document to be created | yes |
    | doc | dict | Document content | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains the ID and revision of the created document |

=== "JSON"

    ```json
    {
        "create_collection": {
            "db_name": "couch2",
            "doc_id": "test_doc",
            "doc": {"name": "John Doe", "age": 30, "email": "johndoe@example.com"}
        }
    }
    ```

### `update_one`

**update_one**: This function updates a single document in the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | doc_id | str | ID of the document to be updated | yes |
    | data | dict | New data to update the document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains the ID and new revision of the updated document |

=== "JSON"

    ```json
    {
        "update_one": {
            "db_name": "couch2",
            "doc_id": "test_doc",
            "data": {"name": "Jane Doe"}
        }
    }
    ```

### `update_many`

**update_many**: This function updates multiple documents in the specified database based on a query.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | query | dict | Query to select documents for update | yes |
    | docs | dict | New data to update the selected documents | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains the number of documents updated |

=== "JSON"

    ```json
    {
        "update_many": {
            "db_name": "couch2",
            "query": {"name": "J[a-z].*e"},
            "docs": {"name": "Minnie Sharma"}
        }
    }
    ```

### `find`

**find**: This function finds documents in the specified database based on a selector.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | selector | dict | Selector to filter documents | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of documents matching the selector |

=== "JSON"

    ```json
    {
        "find": {
            "db_name": "couch2",
            "selector": {"age": {"$gt": 12}}
        }
    }
    ```

### `find_all`

**find_all**: This function retrieves all documents from the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all documents in the database |

=== "JSON"

    ```json
    {
        "find_all": {
            "db_name": "couch2"
        }
    }
    ```

### `select_distinct`

**select_distinct**: This function retrieves distinct values for a specified field in the database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | field | str | Field name to get distinct values | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of distinct values for the specified field |

=== "JSON"

    ```json
    {
        "select_distinct": {
            "db_name": "couch2",
            "field": "name"
        }
    }
    ```

### `get_all_documents`

**get_all_documents**: This function retrieves all documents from the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all documents in the database |

=== "JSON"

    ```json
    {
        "get_all_documents": {
            "db_name": "couch2"
        }
    }
    ```

### `insert_many`

**insert_many**: This function inserts multiple documents into the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | data | list | List of documents to be inserted | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of results for each inserted document |

=== "JSON"

    ```json
    {
        "insert_many": {
            "db_name": "couch2",
            "data": [
                {"name": "Alice", "age": 25},
                {"name": "Bob Smith", "age": 45},
                {"name": "Charlie Smith", "age": 55}
            ]
        }
    }
    ```

### `replace_one`

**replace_one**: This function replaces a single document in the specified database based on a query.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | query | dict | Query to select the document for replacement | yes |
    | replace | dict | New document to replace the old one | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains the ID and new revision of the replaced document |

=== "JSON"

    ```json
    {
        "replace_one": {
            "db_name": "couch2",
            "query": {"name": "M[a-z].*e"},
            "replace": {"name": "Jack"}
        }
    }
    ```

### `delete_one`

**delete_one**: This function deletes a single document from the specified database based on a query.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | query | dict | Query to select the document for deletion | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the document is deleted successfully |

=== "JSON"

    ```json
    {
        "delete_one": {
            "db_name": "couch2",
            "query": {"name": "Jack Sharma"}
        }
    }
    ```

### `delete_all`

**delete_all**: This function deletes all documents from the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if all documents are deleted successfully |

=== "JSON"

    ```json
    {
        "delete_all": {
            "db_name": "couch2"
        }
    }
    ```

### `delete_many`

**delete_many**: This function deletes multiple documents from the specified database based on a query.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | db_name | str | Name of the database | yes |
    | query | dict | Query to select documents for deletion | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Number of documents deleted |

=== "JSON"

    ```json
    {
        "delete_many": {
            "db_name": "couch2",
            "query": {"name": ".*Smith"}
        }
    }
    ```

### `delete_database`

**delete_database**: This function deletes the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | database | str | Name of the database to be deleted | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the database is deleted successfully |

=== "JSON"

    ```json
    {
        "delete_database": {
            "database": "couch2"
        }
    }
    ```

### `drop_connection`

**drop_connection**: This function closes the active database connection.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the connection is closed successfully |

=== "JSON"

    ```json
    {
        "drop_connection": {}
    }
    ```

---

## Frequently Asked Questions

### How do I configure CouchDB credentials in EasyTask?
Use the EasyTask vault system to securely store your CouchDB connection credentials. Navigate to the integration configuration page and add your host, port, username, and password under a vault key like `couchdb/secret`.

### Can I use CouchDB with both EasyTask Cloud and On-Premises?
Yes, CouchDB works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot CouchDB connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your host, port, and credentials in the vault, ensure the CouchDB server is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
