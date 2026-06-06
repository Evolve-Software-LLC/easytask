---
title: SSH - EasyTask Integration Guide
description: Connect SSH with EasyTask for automated remote command execution, file transfer, and server management in scheduled workflows.
keywords:
  - ssh
  - easytask
  - workflow orchestration
  - automation
  - remote command execution
  - file transfer
  - ssh integration
  - server management
---

# SSH Integration

SSH (Secure Shell) is a cryptographic network protocol used for secure remote login, command execution, and file transfer between networked computers. It provides a secure channel over an unsecured network by encrypting all traffic, making it the industry standard for remote server administration, automated deployments, and infrastructure management.

## Why Integrate SSH with EasyTask?

SSH is the backbone of remote server administration and DevOps automation. By integrating SSH with EasyTask, you can automate remote command execution, file transfers, and server health checks on a configurable schedule — all without manual login. EasyTask enables you to execute shell commands on remote servers, transfer files between systems, check service statuses, and perform routine maintenance tasks through scheduled workflows. With EasyTask's vault-based credential management, your SSH private keys and connection details remain encrypted and secure while enabling hands-free server operations.

## Integration Server Vault details

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "host": "xx.x.xx.xxx",
        "password": "*******",
        "port": "22",
        "username": "admin"
      }
    }
    ```

### SSH JSON Format

An SSH instance can be created as below by passing the vault_path_key:

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "ssh") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing SSH credentials | Yes |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of SSH

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
              "integration": "ssh",
              "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
              "init": {
                  "vault_path_key": "ssh/server1"
              },
              "action": [
                  {
                      "execute_command": {
                          "command": "df -h"
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
          "execute_command": {
            "exit_code": 0,
            "stdout": "Filesystem      Size  Used Avail Use% Mounted on\n/dev/sda1        50G   20G   28G  42% /",
            "stderr": ""
          }
        }
    }
    ```

## Available Functions

| Function | Description |
|----------|-------------|
| `execute_command` | Execute a shell command on a remote server via SSH |
| `upload_file` | Upload a file from the local system to the remote server |
| `download_file` | Download a file from the remote server to the local system |
| `check_connection` | Verify SSH connectivity to the remote server |
| `get_system_info` | Retrieve system information from the remote server |
| `list_directory` | List files and directories on the remote server |

### `execute_command`

**Execute a remote command via SSH**:

This function executes a shell command on the remote server and returns the output.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | command | string | The shell command to execute on the remote server | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "execute_command": {
                "command": "uptime"
              }
            }
          ]
        }
      ]
    }
    ```

### `upload_file`

**Upload a file to the remote server**:

This function transfers a file from the local system to the remote server via SFTP/SCP.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | local_path | string | Path to the local file to upload | Yes |
    | remote_path | string | Destination path on the remote server | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "upload_file": {
                "local_path": "/home/user/report.csv",
                "remote_path": "/tmp/report.csv"
              }
            }
          ]
        }
      ]
    }
    ```

### `download_file`

**Download a file from the remote server**:

This function transfers a file from the remote server to the local system via SFTP/SCP.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | remote_path | string | Path to the file on the remote server | Yes |
    | local_path | string | Destination path on the local system | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "download_file": {
                "remote_path": "/var/log/app.log",
                "local_path": "/home/user/logs/app.log"
              }
            }
          ]
        }
      ]
    }
    ```

### `check_connection`

**Check SSH connectivity**:

This function verifies that the SSH connection to the remote server is working.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "check_connection": {}
            }
          ]
        }
      ]
    }
    ```

### `get_system_info`

**Get remote system information**:

This function retrieves system information (OS, memory, disk, CPU) from the remote server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "get_system_info": {}
            }
          ]
        }
      ]
    }
    ```

### `list_directory`

**List remote directory contents**:

This function lists the files and directories at a specified path on the remote server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | The directory path to list on the remote server | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | user | string | The username of the user who performed the action |
    | integration | string | The type of integration used (ssh) |
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
          "integration": "ssh",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "ssh/server1"
          },
          "action": [
            {
              "list_directory": {
                "path": "/var/log"
              }
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What authentication methods does the SSH integration support?

The EasyTask SSH integration supports password-based authentication stored securely in the vault. Your SSH credentials (host, port, username, and password) are encrypted at rest in the EasyTask secret store. The vault path key (e.g., `ssh/server1`) references these credentials without exposing them in task configurations.

### Can I run multiple commands in a single SSH task?

Yes. You can chain multiple actions within a single SSH integration task. Each action in the `action` array is executed sequentially against the remote server. For example, you can check disk usage, restart a service, and download a log file — all within the same scheduled task run.

### How does EasyTask handle SSH connection failures?

EasyTask includes built-in error resilience for SSH connections. If a connection fails due to network issues or server unavailability, EasyTask reports the error clearly with details about which action failed and why. You can configure retry logic at the task level to automatically reattempt failed SSH operations, ensuring reliable remote execution even in unstable network conditions.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
