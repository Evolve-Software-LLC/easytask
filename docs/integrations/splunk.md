---
title: Splunk - EasyTask Integration Guide
description: Connect Splunk with EasyTask for automated log indexing, search job management, and data analytics in scheduled workflows.
keywords:
  - splunk
  - easytask
  - workflow orchestration
  - automation
  - log management
  - search analytics
  - splunk integration
---

# Splunk

This integration is an interface to an API for a service called "Splunk". Splunk is a server application that is used mainly for saving, indexing, searching through and mannage log file data. This integration allows us to comunicate with such servers. The API used by the integration as of now is splunklib.

Splunk has a lot of features, but for now the integration only supports key features of splunk relating to indixes and jobs. There are 3 types off functions in the integration. Index Functions (for index related functionality), Job Functions (For job related functionality), and Common functions (For functionalies that are comman between the two).

A string of log file data can fed to a splunk index which is then taken as or segmented into an event or multiple events. Then a search job can be created to search any index and its events.
Every index or search job is consedered an "Entity" object, and is stored withen collections such as "jobs" and "indexes". The integration allowes you to access any such Entity and apply some function on it (which internaly happens via a Entity class method or some other way depending on the perticular typpe of function). 

## Why Integrate Splunk with EasyTask?

Splunk is the industry-leading platform for log management, operational intelligence, and security analytics. By integrating Splunk with EasyTask, you can automate index management, search job creation, log ingestion, and data analytics on a configurable schedule. EasyTask enables you to create and manage Splunk indexes, run search queries, control job lifecycles, and extract insights from your log data — all through scheduled workflows. This integration is ideal for automating security monitoring, generating scheduled compliance reports, and building operational dashboards without manual log analysis.

## Integration Server Vault details

## Required secrets in Vault

=== "Table"

    | Key | Type | Description |
    |-----|------|-------------|
    | host | string | The hostname or IP address of the PostgreSQL server |
    | password | string | The password for authentication |
    | port | integer | The port number on which the PostgreSQL server is running |
    | username | string | The username for authentication |

=== "JSON"

    ```json
    {
      "secret": {
        "host": "xxxxxxxx",
        "password": "xxxxxxxx",
        "port": 5432,
        "username": "xxxxxxxx"
      }
    }
    ```

## Initialising Splunk integration object

```py
from libs.easytask.integrations.splunk.splunk_integration import SplunkIntegration

vault_path_key = "splunk/server1"
sb = SplunkIntegration(vault_path_key)
```

## Example cURL Commands

### Sample Usage of Splunk 

=== "Input Command"

    ```sh
    
    curl -X POST "https://your-api-endpoint/execute" \
        -H "Content-Type: application/json" \
        -d '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [
            {
            "integration": "splunk",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "splunk/server1"
            },
            "action": [
                {
                "delete_if_exists": {
                    "collection": "jobs",
                    "entity": "YOUR_JOB_ID_HERE"
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
            "delete_if_exists": false
        }
    }
    ```

## Functions

### `list`

**List entities in a collection (Indices or Jobs)**:

This function lists all the entities of a collection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection ("indexes" or "jobs") | Yes |
    | count | integer | Number of results to see (defaults to None) | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the list action |

=== "Command"

    ```python
    sb.list("indexes")
    ```

### `delete`

**Delete an entity**:

This function deletes an entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.delete("jobs", job)
    ```

### `delete_if_exists`

**Delete entity if it exists**:

This function deletes an entity if it exists. If it does not exist, no error is thrown.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_if_exists action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.delete_if_exists("jobs", job)
    ```

### `refresh`

**Refresh an entity**:

This function refreshes the state of this entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the refresh action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.refresh("jobs", job)
    ```

### `update`

**Update an entity**:

This function updates the server with any changes you've made to the current entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.update("jobs", job)
    ```

### `access`

**Access an entity's metadata**:

This function returns the access metadata for the given entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the access action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.access("jobs", job)
    ```

### `content`

**Returns info on the contents of the given entity**:

This function returns info on the contents of the given entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the content action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.content("jobs", job)
    ```

### `links`

**Get related resources for an entity**:

This function returns a dictionary of related resources.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the links action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.links("jobs", job)
    ```

### `fields`

**Get all data on an entity**:

This function returns the content metadata along with other stuff for this entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the fields action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.fields("jobs", job)
    ```

### `state`

**Get entity state record**:

This function returns the entity's state record.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the state action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.state("jobs", job)
    ```

### `path`

**Get path for the entity within the Splunk server**:

This function returns the path for the given entity.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | collection | string | Name of the collection where the desired entity is | Yes |
    | entity | string | Name of the entity on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the path action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.path("jobs", job)
    ```

### `create_index`

**Create Index**:

This function creates a new index in Splunk.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the index to be created | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_index action |

=== "Command"

    ```python
    sb.create_index("test_index")
    ```

### `write_event`

**Write Event**:

This function opens a stream (a writable socket) to write data to an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | index_name | string | Name of the index on which the function has to be performed | Yes |
    | event_text | string | Text string containing all your events, timestamps, etc. | Yes |
    | source | string | Name of the source of these events | No |
    | sourcetype | string | Tells Splunk how to process event_text | No |
    | timer | integer | Number of seconds to wait after the function is performed | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the write_event action |

=== "Command"

    ```python
    event = "System error2\nRebooting system"
    sb.write_event("test_index", event, "Admin_PC", "backup_file")
    ```

### `submit_event`

**Submit Event**:

This function uses HTTP POST to write to an index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | index_name | string | Name of the index on which the function has to be performed | Yes |
    | event_text | string | Text string containing all your events, timestamps, etc. | Yes |
    | source | string | Name of the source of these events | No |
    | sourcetype | string | Tells Splunk how to process event_text | No |
    | timer | integer | Number of seconds to wait after the function is performed | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the submit_event action |

=== "Command"

    ```python
    event = "System error2\nRebooting system"
    sb.submit_event("test_index", event, "Admin_PC", "backup_file")
    ```

### `clean_index`

**Clean Index**:

This function deletes the contents of the index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | index_name | string | Name of the index on which the function has to be performed | Yes |
    | timeout | integer | The time-out period for the operation, in seconds | No |
    | timer | integer | Number of seconds to wait after the function is performed | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the clean_index action |

=== "Command"

    ```python
    sb.clean_index("test_index")
    ```

### `roll_hot_buckets`

**Roll Hot Buckets**:

This function performs the Roll Hot Buckets operation.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | index_name | string | Name of the index on which the function has to be performed | Yes |
    | timer | integer | Number of seconds to wait after the function is performed | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the roll_hot_buckets action |

=== "Command"

    ```python
    sb.roll_hot_buckets("test_index")
    ```

### `create_job`

**Create Job**:

This function creates a new job with the given search query.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | query | string | The search query | Yes |
    | blocking | boolean | Whether the search runs synchronously | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_job action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    print("#Create_Job:", type(job), job)
    ```

### `get_job_preview`

**Get Job Preview**:

This function returns any results that have been generated so far, whether the job is running or not.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_job_preview action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    output = sb.get_job_preview(job)
    print(output)
    ```

### `cancel_job`

**Cancel Job**:

This function stops the current search and deletes the results cache.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the cancel_job action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.cancel_job(job)
    ```

### `finalize_job`

**Finalize Job**:

This function stops the job and allows for getting intermediate results.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the finalize_job action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.finalize_job(job)
    ```

### `is_job_done`

**Check if job is finished running**:

This function indicates whether this job finished running.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the is_job_done action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.is_job_done(job)
    ```

### `is_job_ready`

**Check if job is ready for querying**:

This function indicates whether this job is ready for querying.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the is_job_ready action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.is_job_ready(job)
    ```

### `pause_job`

**Pause Job**:

This function suspends the current search.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the pause_job action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.pause_job(job)
    ```

### `resume_job`

**Resume a paused job**:

This function resumes the current search, if paused.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the resume_job action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.resume_job(job)
    ```

### `set_job_priority`

**Set job priority**:

This function sets this job's search priority in the range of 0-10.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |
    | value | integer | The search priority | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the set_job_priority action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.set_job_priority(job, 5)
    ```

### `touch_job`

**Set job expiration time to current time**:

This function extends the expiration time of the search to the current time (now) plus the time-to-live (ttl) value.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init |

### `set_job_ttl`

**Set job time to live**:

This function sets the job's time-to-live (ttl) value, which is the time before the search job expires and is still available.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | Name of the job on which the function has to be performed | Yes |
    | value | integer | The ttl value, in seconds | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (splunk) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the set_job_ttl action |

=== "Command"

    ```python
    query = """search index = "test_index" """
    job = sb.create_job(query)
    sb.set_job_ttl(job, 50)
    ```

## FAQ

### What Splunk operations does EasyTask support?

EasyTask supports Splunk index management (create, delete, list indexes) and search job operations (create jobs, set TTL, retrieve results). Functions are organized into Index Functions, Job Functions, and Common Functions for comprehensive log management automation.

### How do I automate Splunk searches with EasyTask?

Configure your Splunk integration with vault credentials, then use the `create_job` function to define search queries within scheduled tasks. You can automate periodic log analysis, generate compliance reports, and trigger alerts based on search results — all on configurable schedules.

### Does the Splunk integration support real-time log ingestion?

Yes. The Splunk integration allows you to feed log data into Splunk indexes programmatically. Combined with EasyTask scheduling, you can automate log ingestion from multiple sources, manage index lifecycles, and ensure your Splunk environment stays up to date without manual data forwarding.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
