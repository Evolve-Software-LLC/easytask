---
description: Elasticsearch integration for EasyTask — automate document indexing, search queries, and index management in scheduled workflows.
keywords:
  - Elasticsearch automation
  - search indexing
  - log analytics scheduling
  - EasyTask Elasticsearch
  - document indexing
  - SQL queries Elasticsearch
---

# Elasticsearch API

The Elasticsearch API provides a set of operations for interacting with Elasticsearch, allowing users to index, search, update, and delete documents.

## Why Integrate Elasticsearch with EasyTask?

Elasticsearch is a distributed search and analytics engine built for scalability, speed, and relevance. By integrating Elasticsearch with EasyTask, you can automate document indexing, run complex search queries, manage indices, and perform SQL queries — all on a scheduled basis within your workflows. This integration is ideal for log analytics, content search, real-time data processing, and any use case that demands reliable, automated interaction with your Elasticsearch cluster.

## Required Values in Vault

```
{
   "secret": {
      "host": "http://XXX.XXX.XXX.XXX:YYYY"
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
        "integration": "elasticsearch",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "elasticsearch/secret"
        },
        "action": [
            {
                "index_document": {
                    "index": "new_index",
                    "id": 3,
                    "body": {
                        "name": "hello,this is the new index"
                    }
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
   
    {

        "integration": "elastic_search",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "elasticsearch/server1"
        },
        "error": false,
        "action": [
            {
                "index_document": {
                    "_index": "new_index",
                    "_id": "3",
                    "_version": 17,
                    "result": "updated",
                    "_shards": {
                        "total": 2,
                        "successful": 1,
                        "failed": 0
                    },
                    "_seq_no": 16,
                    "_primary_term": 1
                }
            }
        ]
    }

    ```

## Functions

### `index_document`

**index_document**: This function indexes a document in Elasticsearch.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document | yes |
    | body | dict | Document content | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the indexed document |

=== "JSON"

    ```json
    {
        "index_document": {
            "index": "new_index",
            "id": 3,
            "body": {
                "name": "hello,this is the new index"
            }
        }
    }
    ```

### `exists`

**exists**: This function checks if a document exists in an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the document exists, False otherwise |

=== "JSON"

    ```json
    {
        "exists": {
            "index": "new_index",
            "id": 3
        }
    }
    ```

### `get_all_indices`

**get_all_indices**: This function retrieves all indices in the Elasticsearch cluster.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all index names |

=== "JSON"

    ```json
    {
        "get_all_indices": {}
    }
    ```

### `get_document`

**get_document**: This function retrieves a document from an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Document content |

=== "JSON"

    ```json
    {
        "get_document": {
            "index": "new_index",
            "id": 3
        }
    }
    ```

### `refresh_index`

**refresh_index**: This function refreshes an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index to refresh | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the refresh operation |

=== "JSON"

    ```json
    {
        "refresh_index": {
            "index": "new_index"
        }
    }
    ```

### `search_document`

**search_document**: This function searches for documents in an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index to search | yes |
    | query | dict | Elasticsearch query | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Search results |

=== "JSON"

    ```json
    {
        "search_document": {
            "index": "new_index",
            "query": {
                "match_all": {}
            }
        }
    }
    ```

### `exact_match`

**exact_match**: This function performs an exact match search in an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index to search | yes |
    | query | dict | Exact match query | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Search results |

=== "JSON"

    ```json
    {
        "exact_match": {
            "index": "new_index",
            "query": {
                "name": "hello,this is the new index"
            }
        }
    }
    ```

### `update_document`

**update_document**: This function updates a document in an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document to update | yes |
    | body | dict | Updated document content | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the update operation |

=== "JSON"

    ```json
    {
        "update_document": {
            "index": "new_index",
            "id": 3,
            "body": {
                "name": "new content updated"
            }
        }
    }
    ```

### `execute_with_sql`

**execute_with_sql**: This function executes an SQL query against Elasticsearch.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | query | str | SQL query to execute | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Query results |

=== "JSON"

    ```json
    {
        "execute_with_sql": {
            "query": "SELECT * FROM new_index"
        }
    }
    ```

### `get_last_modified`

**get_last_modified**: This function retrieves the last modified timestamp of a document.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Last modified timestamp |

=== "JSON"

    ```json
    {
        "get_last_modified": {
            "index": "new_index",
            "id": 3
        }
    }
    ```

### `delete_document`

**delete_document**: This function deletes a document from an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | index | str | Name of the index | yes |
    | id | int/str | ID of the document to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the delete operation |

=== "JSON"

    ```json
    {
        "delete_document": {
            "index": "new_index",
            "id": 3
        }
    }
    ```

## FAQ

### What Elasticsearch operations does EasyTask support?

EasyTask supports a wide range of Elasticsearch operations including indexing documents (`index_document`), retrieving documents (`get_document`), searching documents (`search_document`, `exact_match`), updating documents (`update_document`), deleting documents (`delete_document`), listing all indices (`get_all_indices`), refreshing indices (`refresh_index`), executing SQL queries (`execute_with_sql`), and checking document existence (`exists`) as well as retrieving last modified timestamps (`get_last_modified`).

### How do I index documents in scheduled workflows?

To index documents on a schedule, create a task in EasyTask that uses the `index_document` action. Provide the target index name, a unique document ID, and the document body as a JSON dictionary. Store your Elasticsearch host credentials in the EasyTask vault, reference the vault path in the task configuration, and set the desired schedule. EasyTask will automatically index the document at the configured intervals.

### Can I run SQL queries against Elasticsearch?

Yes. EasyTask provides the `execute_with_sql` function, which allows you to run SQL queries directly against your Elasticsearch cluster. Pass a standard SQL query string (e.g., `SELECT * FROM my_index`) and EasyTask will return the results, making it easy to extract and analyze data without writing native Elasticsearch DSL queries.

## Next Steps

- [Introduction to Integrations](integrations_intro.md)
- [Datadog Integration](datadogs.md)
- [PostgreSQL Integration](postgresql.md)
