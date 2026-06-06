---
description: "MongoDB integration for document database operations in scheduled workflows. Automate CRUD, collection management, and document processing with EasyTask."
keywords:
  - MongoDB task scheduling
  - NoSQL automation
  - document database
  - MongoDB CRUD operations
  - scheduled database tasks
---

# MongoDB API

The MongoDB API provides a set of operations for interacting with MongoDB databases, allowing users to create databases and collections, insert, update, find, and delete documents.

## Why Integrate MongoDB with EasyTask?

MongoDB is a leading NoSQL document database, prized for its flexibility, scalability, and JSON-like document model. By integrating MongoDB with EasyTask, you can automate scheduled CRUD operations, collection management, and document data processing at scale. This integration is ideal for content management systems, IoT data ingestion pipelines, application data workflows, and any scenario where structured or semi-structured data needs to be reliably stored, queried, and maintained on a recurring schedule.

## Required Values in Vault

```
{
   "secret": {
      "database_name": "xxx...",
      "mongo_hook": "xxx",
      "mongo_host": "xxx.xxx.xx.x",
      "mongo_password": "*******",
      "mongo_port": "xxxx",
      "mongo_user": "xxxxx"
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
        "integration": "mongodb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "mongodb/secret"
        },
        "action": [
            {
                "create_database": {
                    "database": "my_database"
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "user": "test user",
        "integration": "mongodb",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "mongo/server1"
        },
        "error": false,
        "action": [
            {
                {
                    "create_database": "Database(MongoClient(host=['192.158.238.91:27017'], document_class=dict, tz_aware=False, connect=True), 'my_database')"
                }
            }
        ]
    }

    ```

## Functions

### `create_database`

**create_database**: This function creates a new database in MongoDB.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | database | str | Name of the database to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the database was created successfully |

=== "JSON"

    ```json
    {
        "create_database": {
            "database": "my_database"
        }
    }
    ```

### `create_collection`

**create_collection**: This function creates a new collection in the specified database.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the collection was created successfully |

=== "JSON"

    ```json
    {
        "create_collection": {
            "coll_name": "client_db"
        }
    }
    ```

### `insert_one`

**insert_one**: This function inserts a single document into a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | records | dict | Document to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | ID of the inserted document |

=== "JSON"

    ```json
    {
        "insert_one": {
            "coll_name": "client_db",
            "records": {
                "name": "John",
                "age": 25
            }
        }
    }
    ```

### `insert_many`

**insert_many**: This function inserts multiple documents into a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | records | list | List of documents to insert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of IDs of the inserted documents |

=== "JSON"

    ```json
    {
        "insert_many": {
            "coll_name": "client_db",
            "records": [
                {
                    "name": "Adam",
                    "age": 30
                },
                {
                    "name": "Jason",
                    "age": 14
                }
            ]
        }
    }
    ```

### `update_one`

**update_one**: This function updates a single document in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | where | dict | Filter to select the document to update | yes |
    | values | dict | New values to set | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the update operation |

=== "JSON"

    ```json
    {
        "update_one": {
            "coll_name": "client_db",
            "where": {
                "name": "John"
            },
            "values": {
                "name": "Vicky"
            }
        }
    }
    ```

### `update_many`

**update_many**: This function updates multiple documents in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | where | dict | Filter to select the documents to update | yes |
    | values | dict | New values to set | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the update operation |

=== "JSON"

    ```json
    {
        "update_many": {
            "coll_name": "client_db",
            "where": {
                "address": {
                    "$regex": "^S"
                }
            },
            "values": {
                "name": "Minnie"
            }
        }
    }
    ```

### `replace_one`

**replace_one**: This function replaces a single document in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | where | dict | Filter to select the document to replace | yes |
    | values | dict | New document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the replace operation |

=== "JSON"

    ```json
    {
        "replace_one": {
            "coll_name": "client_db",
            "where": {
                "name": "John"
            },
            "values": {
                "name": "Harry"
            }
        }
    }
    ```

### `find_one`

**find_one**: This function finds a single document in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | where | dict | Filter to select the document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | The found document |

=== "JSON"

    ```json
    {
        "find_one": {
            "coll_name": "client_db",
            "where": {
                "name": "Adam"
            }
        }
    }
    ```

### `find_all`

**find_all**: This function finds all documents in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all documents in the collection |

=== "JSON"

    ```json
    {
        "find_all": {
            "coll_name": "client_db"
        }
    }
    ```

### `select_distinct`

**select_distinct**: This function finds distinct values for a specified field in a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | field_name | str | Field to find distinct values for | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of distinct values |

=== "JSON"

    ```json
    {
        "select_distinct": {
            "coll_name": "client_db",
            "field_name": "name"
        }
    }
    ```

### `delete_one`

**delete_one**: This function deletes a single document from a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | where | dict | Filter to select the document to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the delete operation |

=== "JSON"

    ```json
    {
        "delete_one": {
            "coll_name": "client_db",
            "where": {
                "name": "xyz"
            }
        }
    }
    ```

### `delete_many`

**delete_many**: This function deletes multiple documents from a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |
    | query | dict | Filter to select the documents to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the delete operation |

=== "JSON"

    ```json
    {
        "delete_many": {
            "coll_name": "client_db",
            "query": {
                "name": "xyz"
            }
        }
    }
    ```

### `delete_all`

**delete_all**: This function deletes all documents from a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the delete operation |

=== "JSON"

    ```json
    {
        "delete_all": {
            "coll_name": "client_db"
        }
    }
    ```

### `drop_collection`

**drop_collection**: This function drops (deletes) a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | coll_name | str | Name of the collection to drop | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the collection was dropped successfully |

=== "JSON"

    ```json
    {
        "drop_collection": {
            "coll_name": "client_db"
        }
    }
    ```

## FAQ

### What MongoDB operations does EasyTask support?

EasyTask supports a comprehensive set of MongoDB operations including `create_database`, `create_collection`, `insert_one`, `insert_many`, `update_one`, `update_many`, `replace_one`, `find_one`, `find_all`, `select_distinct`, `delete_one`, `delete_many`, `delete_all`, and `drop_collection`. These cover the full range of CRUD operations, collection management, and document querying.

### How do I insert documents in scheduled workflows?

You can use the `insert_one` action to insert a single document or `insert_many` to insert multiple documents at once. Define the collection name and the document data in the action JSON, then schedule the task through EasyTask. Credentials and connection details are securely stored in the Vault and referenced via `vault_path_key`.

### Can I query and filter MongoDB collections?

Yes. Use `find_one` to retrieve a single document matching a filter, `find_all` to retrieve all documents in a collection, or `select_distinct` to get unique values for a specific field. Filters are passed as a `where` dictionary supporting MongoDB query operators such as `$regex` for pattern matching.

## Next Steps

- [Integrations Overview](integrations_intro.md) -- Explore all available EasyTask integrations.
- [PostgreSQL Integration](postgresql.md) -- Schedule tasks for relational database operations.
- [Redis Integration](redis.md) -- Automate caching and key-value store operations.
