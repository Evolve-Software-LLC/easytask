---
description: Learn how to integrate Redis with EasyTask for caching, data structure manipulation, and pub/sub messaging in your scheduled tasks.
keywords: [Redis task scheduling, Redis cache automation, Redis pub/sub scheduled tasks, EasyTask Redis integration, Redis data structures workflow]
---

# Redis

Redis (Remote Dictionary Server) is an open-source, in-memory data structure store that can be used as a database, cache, and message broker. It supports various data structures like strings, hashes, lists, sets, and more, offering high-speed operations and scalability.

## Why Integrate Redis with EasyTask?

Redis is a powerful in-memory data store that excels at caching, real-time analytics, and message brokering. By integrating Redis with EasyTask, your scheduled tasks can directly manipulate Redis data structures — including hashes, lists, and sets — as well as interact with pub/sub channels to build event-driven workflows. This makes it a perfect fit for use cases like session management, rate limiting, real-time data processing, and cache automation, all triggered on a schedule or as part of a larger task pipeline.

## Integration Server Vault details

#### Require Secrets in Vault

=== "Table"

    | Key | Description |
    |-----|-------------|
    | redis_host | The hostname or IP address of the Redis server |
    | redis_password | The password for connecting to the Redis server |
    | redis_port | The port number on which the Redis server is running |

=== "JSON"

    ```json
    {
      "secret": {
        "redis_host": "xxx.xxx.xxx.xx",
        "redis_password": "**********",
        "redis_port": "xxxx"
      }
    }
    ```

### Redis Integration JSON Format

=== "Table"

    | Key | Description |
    |-----|-------------|
    | is_credentials | Object containing user credentials |
    | integrations | Array of integration objects |
    | integration | Type of integration (redis in this case) |
    | uuid | Unique identifier for the integration instance |
    | init | Initialization parameters |
    | vault_path_key | Path to the vault containing Redis credentials |
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
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of Redis

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
                "integration": "redis",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "redis/server1"
                },
                "action": [
                    {
                        "hget": {
                            "name": "fullname",
                            "key": "firstname"
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
            "hget": "john_doe"
        }
    }
    ```

## Functions

### `hset`

**Create a Hash**:

This function sets a hash value for a specific key in Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Hash name | Yes |
    | key | string | Key value | Yes |
    | value | string | Value for the key | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the hset action |

    The `hset` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | hset | int | 1 if hash is created successfully, 0 otherwise |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "hset": {
                "name": "fullname",
                "key": "firstname",
                "value": "john_doe"
              }
            }
          ]
        }
      ]
    }
    ```

### `hgetall`

**Fetch all key-values of a Hash**:

This function retrieves all elements in a hash from Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Hash name | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the hgetall action |

    The `hgetall` result is an object:

    | Field | Type | Description |
    |-------|------|-------------|
    | hgetall | object | Key-value pairs of all fields and values in the hash |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "hgetall": {
                "name": "fullname"
              }
            }
          ]
        }
      ]
    }
    ```

### `hget`

**Fetch a value by key from Hash**:

This function retrieves an element by key from a hash in Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Hash name | Yes |
    | key | string | Hash key | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the hget action |

    The `hget` result can be any type:

    | Field | Type | Description |
    |-------|------|-------------|
    | hget | any | Value associated with the key, or null if not found |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "hget": {
                "name": "fullname",
                "key": "firstname"
              }
            }
          ]
        }
      ]
    }
    ```

### `lpush`

**Create a List And Left Push**:

This function pushes values onto the head of a list in Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of list | Yes |
    | values | array | Values to push onto the list | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the lpush action |

    The `lpush` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | lpush | int | Length of the list after the push operation |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "lpush": {
                "name": "backend",
                "values": [
                  "Django",
                  "mysql",
                  "mongodb",
                  "oracle"
                ]
              }
            }
          ]
        }
      ]
    }
    ```

### `lrange`

**Fetch elements from a list for a range**:

This function retrieves list elements in a given range from Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | start | integer | List start index | Yes |
    | end | integer | List end index | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the lrange action |

    The `lrange` result is an array:

    | Field | Type | Description |
    |-------|------|-------------|
    | lrange | array | List of elements in the specified range |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "lrange": {
                "name": "backend",
                "start": 0,
                "end": -1
              }
            }
          ]
        }
      ]
    }
    ```

### `lset`

**Set an Element in List**:

This function sets the value of an element in a Redis list by its index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | index | integer | Index of the element to set | Yes |
    | value | any | Value to set at the specified index | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the lset action |

    The `lset` result is a boolean:

    | Field | Type | Description |
    |-------|------|-------------|
    | lset | boolean | true if the operation was successful, false otherwise |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "lset": {
                "name": "backend",
                "index": 1,
                "value": "Redis"
              }
            }
          ]
        }
      ]
    }
    ```

### `lindex`

**Get an Element of List by index**:

This function retrieves an element from a Redis list by its index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | index | integer | Index of the element to retrieve | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the lindex action |

    The `lindex` result can be any type:

    | Field | Type | Description |
    |-------|------|-------------|
    | lindex | any | The value at the specified index, or null if index is out of range |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "lindex": {
                "name": "backend",
                "index": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `llen`

**Fetch Length of List**:

This function returns the length of a Redis list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the llen action |

    The `llen` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | llen | integer | The length of the list |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "llen": {
                "name": "backend"
              }
            }
          ]
        }
      ]
    }
    ```

### `lpop`

**Left pop from List**:

This function removes and returns the first elements of the Redis list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | count | integer | Number of elements to pop (optional) | No |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the lpop action |

    The `lpop` result can be any type or an array:

    | Field | Type | Description |
    |-------|------|-------------|
    | lpop | any/array | The popped value(s), or null if the key doesn't exist |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "lpop": {
                "name": "backend",
                "count": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `rpush`

**Push a Element into a List from the Right**:

This function pushes values onto the tail of a Redis list.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | values | array | Values to push onto the list | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the rpush action |

    The `rpush` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | rpush | integer | The length of the list after the push operation |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "rpush": {
                "name": "backend",
                "values": ["sqlite"]
              }
            }
          ]
        }
      ]
    }
    ```

### `popindex`

**Pop value by Index from List**:

This function removes and returns an element from a Redis list by its index.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | List name | Yes |
    | index | integer | Index of the element to pop | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the popindex action |

    The `popindex` result can be any type:

    | Field | Type | Description |
    |-------|------|-------------|
    | popindex | any | The value at the specified index that was removed |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "popindex": {
                "name": "backend",
                "index": 0
              }
            }
          ]
        }
      ]
    }
    ```

### `sadd`

**Create a Set**:

This function adds values to a Redis set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Set name | Yes |
    | values | array | Values to be added to the set | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the sadd action |

    The `sadd` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | sadd | integer | The number of elements added to the set (not including already existing elements) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "sadd": {
                "name": "u1",
                "values": ["abc", "david"]
              }
            }
          ]
        }
      ]
    }
    ```

### `scard`

**Fetch length of Set**:

This function returns the number of elements in a Redis set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the scard action |

    The `scard` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | scard | integer | The number of elements in the set |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "scard": {
                "name": "names"
              }
            }
          ]
        }
      ]
    }
    ```

### `smembers`

**Fetch all elements of Set**:

This function returns all members of a Redis set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the smembers action |

    The `smembers` result is a set:

    | Field | Type | Description |
    |-------|------|-------------|
    | smembers | set | All elements of the set |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "smembers": {
                "name": "names"
              }
            }
          ]
        }
      ]
    }
    ```

### `sismember`

**Check Element in Set**:

This function checks if a value is a member of a Redis set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |
    | value | string | Value to check for in the set | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the sismember action |

    The `sismember` result is a boolean:

    | Field | Type | Description |
    |-------|------|-------------|
    | sismember | boolean | True if the value is in the set, false otherwise |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "sismember": {
                "name": "names",
                "value": "abc"
              }
            }
          ]
        }
      ]
    }
    ```

### `spop`

**Pop Value From Set**:

This function removes and returns a random member from a Redis set.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the spop action |

    The `spop` result can be any type:

    | Field | Type | Description |
    |-------|------|-------------|
    | spop | any | The removed element, or null if the set is empty |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "spop": {
                "name": "names"
              }
            }
          ]
        }
      ]
    }
    ```

### `sunion`

**Union of Sets**:

This function returns the union of specified Redis sets.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |
    | args | array | Names of sets to union | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the sunion action |

    The `sunion` result is a set:

    | Field | Type | Description |
    |-------|------|-------------|
    | sunion | set | The union of the specified sets |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "sunion": {
                "name": "this is a string",
                "args": ["u1", "u2"]
              }
            }
          ]
        }
      ]
    }
    ```

### `sinter`

**Intersection of Sets**:

This function returns the intersection of specified Redis sets.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |
    | args | array | Names of sets to intersect | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the sinter action |

    The `sinter` result is a set:

    | Field | Type | Description |
    |-------|------|-------------|
    | sinter | set | The intersection of the specified sets |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "sinter": {
                "name": "this is a string",
                "args": ["u1", "u2"]
              }
            }
          ]
        }
      ]
    }
    ```

### `sdiff`

**Difference of Sets**:

This function returns the difference of specified Redis sets.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | name | string | Name of the set | Yes |
    | args | array | Names of sets to difference | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the sdiff action |

    The `sdiff` result is a set:

    | Field | Type | Description |
    |-------|------|-------------|
    | sdiff | set | The difference of the specified sets |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "sdiff": {
                "name": "this is a string",
                "args": ["u1", "u2"]
              }
            }
          ]
        }
      ]
    }
    ```

### `subscribe`

**Subscribe to a Channel**:

This function subscribes to a Redis channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | is_tested | boolean | Description not provided | No (defaults to False) |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the subscribe action |

    The `subscribe` result is a string:

    | Field | Type | Description |
    |-------|------|-------------|
    | subscribe | string | "None" (The actual subscription result is not returned) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "subscribe": {
                "channel": "test",
                "is_tested": true
              }
            }
          ]
        }
      ]
    }
    ```

### `publish`

**Publish message to channel**:

This function publishes a message to a Redis channel.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | channel | string | Channel name | Yes |
    | message | string | Message to be sent | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the publish action |

    The `publish` result is a string:

    | Field | Type | Description |
    |-------|------|-------------|
    | publish | string | "None" (The actual number of subscribers the message was delivered to is not returned) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "publish": {
                "channel": "test",
                "message": "hi"
              }
            }
          ]
        }
      ]
    }
    ```

### `flushall`

**Flush all Key Value Pairs**:

This function deletes all the keys of all existing databases in Redis.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (redis) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the flushall action |

    The `flushall` result is a boolean:

    | Field | Type | Description |
    |-------|------|-------------|
    | flushall | boolean | true if the operation was successful |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "redis",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "redis/server1"
          },
          "action": [
            {
              "flushall": {}
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What Redis operations does EasyTask support?

EasyTask supports a wide range of Redis operations including hash operations (`hset`, `hget`, `hgetall`), list operations (`lpush`, `rpush`, `lrange`, `lset`, `lindex`, `llen`, `lpop`, `popindex`), set operations (`sadd`, `scard`, `smembers`, `sismember`, `spop`, `sunion`, `sinter`, `sdiff`), pub/sub operations (`subscribe`, `publish`), and utility operations like `flushall`. These can all be used as actions within your scheduled task integrations.

### How does pub/sub work with scheduled tasks?

EasyTask allows scheduled tasks to publish messages to Redis channels using the `publish` action and subscribe to channels using the `subscribe` action. This enables event-driven architectures where a scheduled task can broadcast events to multiple subscribers, or react to messages published on specific channels — ideal for real-time notifications, inter-service communication, and triggering downstream workflows.

### Can I use Redis hash, list, and set operations in workflows?

Yes. EasyTask provides full support for Redis data structure operations within your task workflows. You can create and read hashes (`hset`, `hget`, `hgetall`), manage lists (`lpush`, `rpush`, `lpop`, `lrange`, `lset`, `lindex`, `llen`, `popindex`), and perform set operations (`sadd`, `scard`, `smembers`, `sismember`, `spop`, `sunion`, `sinter`, `sdiff`). Multiple Redis actions can be chained in a single task definition to build complex data manipulation pipelines.

## Next Steps

- [Introduction to Integrations](integrations_intro.md) — Learn how integrations work in EasyTask.
- [Kafka Integration](kafka.md) — Explore Apache Kafka for high-throughput event streaming.
- [RabbitMQ Integration](rabbitmq.md) — Use RabbitMQ for robust message queuing in your workflows.

