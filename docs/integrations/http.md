---
title: HTTP - EasyTask Integration Guide
description: Connect HTTP with EasyTask for automated web request orchestration. Step-by-step setup, configuration, and best practices for HTTP integration.
keywords:
  - http
  - easytask
  - workflow orchestration
  - automation
  - rest api
  - web requests
---

# HTTP

The Hypertext Transfer Protocol (HTTP) is the foundation of the World Wide Web, and is used to load web pages using hypertext links. HTTP is an application layer protocol designed to transfer information between networked devices and runs on top of other layers of the network protocol stack.

## Why Integrate HTTP with EasyTask?

Integrating HTTP with EasyTask enables you to automate web interactions and API calls within your workflows. This integration allows you to:

- **Automate API Interactions**: Execute GET, POST, PUT, PATCH, DELETE, HEAD, and OPTIONS requests programmatically across your workflow pipeline.
- **Orchestrate Multi-Service Workflows**: Chain HTTP calls to different services and APIs as part of complex, automated business processes.
- **Centralize Endpoint Management**: Store server URLs and authentication credentials securely in the EasyTask vault for consistent, reusable HTTP configurations.

## Integration Server Vault details

### Required secrets in Vault

=== "Table"

    | Key | Description |
    |-----|-------------|
    | password | The password for authentication |
    | port | The port number for the HTTP connection |
    | server | The server address or hostname |
    | user | The username for authentication |

=== "JSON"

    ```json
    {
      "secret": {
        "password": "********",
        "port": "XXXX",
        "server": "XXXXXXXX",
        "user": "example_user"
      }
    }
    ```

###  HTTP integration Json Format

=== "Table"

    | Key | Description |
    |-----|-------------|
    | is_credentials | Object containing user credentials |
    | integrations | Array of integration objects |
    | integration | Type of integration (http in this case) |
    | uuid | Unique identifier for the integration instance |
    | init | Initialization parameters |
    | vault_path_key | Path to the vault containing HTTP credentials |
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
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of HTTP 

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
              "integration": "http",
              "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
              "init": {
                "vault_path_key": "https/server1"
              },
              "action": [
                {
                  "http_get": {
                    "url": "http://httpbin.org:80/get",
                    "data": {
                      "hello": "world"
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
      "http_get": {
          "status_code": 411,
          "headers": {
              "Server": "squid/5.7",
              "Mime-Version": "1.0",
              "Date": "Tue, 12 Mar 2024 10:29:38 GMT",
              "Content-Type": "text/html;charset=utf-8",
              "Content-Length": "4544",
              "X-Squid-Error": "ERR_INVALID_REQ 0",
              "Vary": "Accept-Language",
              "Content-Language": "en",
              "X-Cache": "MISS from ev3-infra-1",
              "X-Cache-Lookup": "NONE from ev3-infra-1:3128",
              "Via": "1.1 ev3-infra-1 (squid/5.7)",
              "Connection": "close"
        }
      }
    }
    ```

## Functions of Http

###  `http_get`

**HTTP GET Request** :

This function sends an HTTP GET request to a specified URL, optionally including query parameters. It returns the response status, headers, and content, allowing for inspection of the server's response.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the GET request to | Yes |
    | data | object | Query parameters to be sent with the request | No |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response details including status code and headers |

=== "JSON"

    ```json
    {
      "is_credentials": {
          "userid": "test",
          "passwd": "test123"
      },
      "integrations": [
          {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
              "vault_path_key": "https/server1"
          },
          "action": [
              {
              "http_get": {
                  "url": "http://httpbin.org:80/get",
                  "data": {
                  "hello": "world"
                  }
              }
              }
          ]
          }
      ]
    }
    ```

### `http_post`

**HTTP POST Request**:

This function sends an HTTP POST request to a specified URL, including a data payload. It returns the response status, allowing for inspection of the server's response to the posted data.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the POST request to | Yes |
    | data | object | Data to be sent in the request body | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": [
            {
              "http_post": {
                "url": "http://httpbin.org:80/post",
                "data": {
                  "hello": "world"
                }
              }
            }
          ]
        }
      ]
     }
    ```

### `http_delete`

**HTTP DELETE Request**:

This function sends an HTTP DELETE request to a specified URL. It returns the response status, allowing for inspection of the server's response to the delete operation.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the DELETE request to | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": [
            {
              "http_delete": {
                "url": "http://httpbin.org:80/delete"
              }
            }
          ]
        }
      ]
    }
    ```

### `http_patch`

**HTTP PATCH Request**:

This function sends an HTTP PATCH request to a specified URL, including a data payload for partial resource modification. It returns the response status, allowing for inspection of the server's response to the patched data.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the PATCH request to | Yes |
    | data | object | Data to be sent in the request body for partial update | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": [
            {
              "http_patch": {
                "url": "http://httpbin.org:80/patch",
                "data": {
                  "hello": "world"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `http_put`

**HTTP PUT Request**:

This function sends an HTTP PUT request to a specified URL, including a data payload for complete resource replacement or creation. It returns the response status, allowing for inspection of the server's response to the put operation.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the PUT request to | Yes |
    | data | object | Data to be sent in the request body | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": [
            {
              "http_put": {
                "url": "http://httpbin.org:80/put",
                "data": {
                  "hello": "world"
                }
              }
            }
          ]
        }
      ]
    }
    
    ```

### `http_head`

**HTTP HEAD Request**:

This function sends an HTTP HEAD request to a specified URL. It returns the response status and headers, allowing for inspection of the server's response metadata without retrieving the body content.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the HEAD request to | Yes |
    | data | object | Query parameters to be sent with the request | No |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code and headers |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "http",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "https/server1"
          },
          "action": [
            {
              "http_head": {
                "url": "http://httpbin.org:80/get",
                "data": {
                  "hello": "world"
                }
              }
            }
          ]
        }
      ]
    }
    
    ```

### `http_options`

**HTTP OPTIONS Request**:

This function sends an HTTP OPTIONS request to a specified URL. It returns the response status and headers, providing information about the communication options available for the target resource.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | url | string | The URL to send the OPTIONS request to | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (http) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the response status code and headers |

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

---

## Frequently Asked Questions

### How do I configure HTTP credentials in EasyTask?
Use the EasyTask vault system to securely store your HTTP connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `https/server1`. Include the server address, port, username, and password.

### Can I use HTTP with both EasyTask Cloud and On-Premises?
Yes, HTTP works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the target HTTP server is reachable from the integration server.

### How do I troubleshoot HTTP connection issues?
Check the integration server logs in EasyTask for detailed error messages, including HTTP status codes and response headers. Verify your credentials in the vault, ensure the target server is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
