---
title: ZooKeeper - EasyTask Integration Guide
description: Connect Apache ZooKeeper with EasyTask for automated configuration management, distributed synchronization, and service discovery in scheduled workflows.
keywords:
  - zookeeper
  - easytask
  - workflow orchestration
  - automation
  - distributed coordination
  - configuration management
  - zookeeper integration
---

# Zookeeper

ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these kinds of services are used in some form or another by distributed applications. Each time they are implemented there is a lot of work that goes into fixing the bugs and race conditions that are inevitable. Because of the difficulty of implementing these kinds of services, applications initially usually skip on them, which make them brittle in the presence of change and difficult to manage. Even when done correctly, different implementations of these services lead to management complexity when the applications are deployed.

## Why Integrate ZooKeeper with EasyTask?

Apache ZooKeeper is the de facto standard for distributed coordination, configuration management, and service discovery in distributed systems. By integrating ZooKeeper with EasyTask, you can automate node management, znode operations, and configuration updates on a configurable schedule. EasyTask enables you to create, read, update, and delete znodes, monitor node states, and orchestrate distributed configuration changes — all triggered by scheduled tasks. This integration is ideal for automating configuration drift detection, scheduling service health checks, and managing distributed application coordination without manual intervention.

## Integration Server vault details

### Required secrets in Vault

=== "Table"

    | Key | Type | Description |
    |-----|------|-------------|
    | host | string | The hostname or IP address of the server |
    | port | string | The port number for the connection |

=== "JSON"

    ```json
    {
      "secret": {
        "host": "xxxxxxxx",
        "port": "xxxxxxxx"
      }
    }
    ```

## Example cURL Commands

### Sample Usage of Zookeeper 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d 
      '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123",
        },
        "integrations": [
            {
                "integration": "zookeeper",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "zookeeper/server1"
                },
                "action": [
                    {
                        "checkIfNodeExists": {
                            "path": "/my/favorite/node"
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
            "checkIfNodeExists": true
        }
    }
    ```

## Functions

### `ensurePath`

**Ensure path**:

This function will recursively create the node and any nodes in the path necessary along the way, but cannot set the data for the node, only the ACL.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to the node | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the ensurePath action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "ensurePath": {
                "path": "/my/favorite"
              }
            }
          ]
        }
      ]
    }
    ```

### `checkIfNodeExists`

**Check if node exists**:

This function checks if a node exists or not. Can be used after creating, updating, or deleting a node to ensure.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to ensure it exists in Zookeeper | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the checkIfNodeExists action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "checkIfNodeExists": {
                "path": "/my/favorite/node"
              }
            }
          ]
        }
      ]
    }
    ```

### `getNodeData`

**Get data**:

This function fetches the data of the node along with detailed node information in a ZnodeStat structure.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to node | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the getNodeData action |

=== "JSON"

    ```sh
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "getNodeData": {
                "path": "/my/favorite/node"
              }
            }
          ]
        }
      ]
    }
    ```

### `createNode`

**Create a new node**:

This function creates a node and can set the data on the node along with a watch function. It requires the path to exist first. Data is encoded in UTF-8 format.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to node | Yes |
    | data | string | Data to be added to the node | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the createNode action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "createNode": {
                "path": "/my/favorite/node",
                "data": "Value1"
              }
            }
          ]
        }
      ]
    }
    ```

### `updateNode`

**Update a node**:

This function updates the data for a given node. A version for the node can be supplied, which will be required to match before updating the data.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to ensure it exists in Zookeeper | Yes |
    | data | string | Data to be updated | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the updateNode action |

=== "JSON"

    ```sh
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "updateNode": {
                "path": "/my/favorite/node",
                "data": "data"
              }
            }
          ]
        }
      ]
    }
    ```

### `getChild`

**Get child of a node**:

This function provides the number of children and all immediate children present on a particular path.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to be checked | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the getChild action |

=== "JSON"

    ```sh
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "getChild": {
                "path": "/my/favorite"
              }
            }
          ]
        }
      ]
    }
    ```

### `deleteNode`

**Delete a node**:

This function deletes a node, and can optionally recursively delete all children of the node as well.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path of the node to be deleted | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the deleteNode action |

=== "JSON"

    ```sh
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "deleteNode": {
                "path": "/my/favorite"
              }
            }
          ]
        }
      ]
    }
    ```

### `stop`

**Stop Module**:

This function instructs the client to drop a connection.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (zookeeper) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the stop action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "zookeeper",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "zookeeper/server1"
          },
          "action": [
            {
              "stop": {}
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What ZooKeeper operations does EasyTask support?

EasyTask supports core ZooKeeper operations including creating, reading, updating, and deleting znodes, starting and stopping ZooKeeper services, managing ACLs, and monitoring node states. You can automate distributed configuration management through scheduled tasks.

### How do I configure ZooKeeper credentials in EasyTask?

Store your ZooKeeper connection details (host and port) in the EasyTask vault using a path key like `zookeeper/server1`. Reference this vault path key in your integration configuration to securely connect to your ZooKeeper ensemble without exposing connection details.

### Can I automate configuration updates across a ZooKeeper ensemble?

Yes. EasyTask enables you to schedule znode updates, batch configuration changes, and coordinate distributed settings across your ZooKeeper ensemble. This is ideal for automating service discovery updates, rolling out configuration changes, and maintaining consistency in distributed systems.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
