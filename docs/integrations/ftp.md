---
title: FTP - EasyTask Integration Guide
description: Connect FTP with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing files and directories on FTP servers.
keywords:
  - ftp
  - easytask
  - workflow orchestration
  - automation
  - file transfer
  - file management
---

# FTP API

The FTP API provides a set of operations for interacting with FTP servers, allowing users to manage files and directories.

## Why Integrate FTP with EasyTask?

Integrating FTP with EasyTask enables you to automate file transfer and server management workflows. This integration allows you to:

- **Automate File Transfers**: Upload and download files to/from FTP servers automatically as part of your EasyTask workflows without manual intervention.
- **Manage Remote Directories**: Create, navigate, and delete directories on FTP servers programmatically through EasyTask orchestration.
- **Monitor File Operations**: Retrieve file sizes, modification times, and directory listings automatically, enabling file monitoring and synchronization workflows.

## Required Values in Vault

```
{
   "secret": {
      "ftp_port": "xxxx",
      "ftp_pwd": "********",
      "ftp_server": "xxx.xxx.xxx.xxx",
      "ftp_user": "abc"
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
        "integration": "ftp",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "ftp/secret"
        },
        "action": [
            {
                "get_connection": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
   
    {
        "integration": "ftp",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "ftp/server1"
        },
        "error": false,
        "action": [
          {
          "get_connection": "220 (vsFTPd 3.0.5) 230 Login successful."
          }
        ]
    }

    ```

## Functions

### `get_connection`

**get_connection**: This function establishes a connection to the FTP server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Connection status message |

=== "JSON"

    ```json
    {
        "get_connection": {}
    }
    ```

### `get_pwd`

**get_pwd**: This function retrieves the current working directory on the FTP server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Current working directory path |

=== "JSON"

    ```json
    {
        "get_pwd": {}
    }
    ```

### `create_dir`

**create_dir**: This function creates a new directory on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | dir_name | str | Name of the directory to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the directory was created successfully |

=== "JSON"

    ```json
    {
        "create_dir": {
            "dir_name": "test_dir_0"
        }
    }
    ```

### `set_cwd`

**set_cwd**: This function changes the current working directory on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | dir_path | str | Path of the directory to change to | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the directory was changed successfully |

=== "JSON"

    ```json
    {
        "set_cwd": {
            "dir_path": "test_dir_0"
        }
    }
    ```

### `delete_dir`

**delete_dir**: This function deletes a directory on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | dir_name | str | Name of the directory to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the directory was deleted successfully |

=== "JSON"

    ```json
    {
        "delete_dir": {
            "dir_name": "test_dir_0"
        }
    }
    ```

### `put_file`

**put_file**: This function uploads a file to the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file to upload | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the file was uploaded successfully |

=== "JSON"

    ```json
    {
        "put_file": {
            "file_name": "readme.txt"
        }
    }
    ```

### `get_file`

**get_file**: This function downloads a file from the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file to download | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the file was downloaded successfully |

=== "JSON"

    ```json
    {
        "get_file": {
            "file_name": "readme.txt"
        }
    }
    ```

### `rename_file`

**rename_file**: This function renames a file on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | from_name | str | Current name of the file | yes |
    | to_name | str | New name for the file | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the file was renamed successfully |

=== "JSON"

    ```json
    {
        "rename_file": {
            "from_name": "readme.txt",
            "to_name": "readme.o"
        }
    }
    ```

### `get_file_size`

**get_file_size**: This function retrieves the size of a file on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Size of the file in bytes |

=== "JSON"

    ```json
    {
        "get_file_size": {
            "file_name": "readme.txt"
        }
    }
    ```

### `get_modified_time`

**get_modified_time**: This function retrieves the last modified time of a file on the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Last modified time of the file |

=== "JSON"

    ```json
    {
        "get_modified_time": {
            "file_name": "readme.txt"
        }
    }
    ```

### `get_dir`

**get_dir**: This function retrieves a detailed directory listing from the FTP server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of file and directory details |

=== "JSON"

    ```json
    {
        "get_dir": {}
    }
    ```

### `get_nlst`

**get_nlst**: This function retrieves a simplified directory listing from the FTP server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of file and directory names |

=== "JSON"

    ```json
    {
        "get_nlst": {}
    }
    ```

### `delete_file`

**delete_file**: This function deletes a file from the FTP server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the file was deleted successfully |

=== "JSON"

    ```json
    {
        "delete_file": {
            "file_name": "readme.txt"
        }
    }
    ```

### `close_connection`

**close_connection**: This function closes the connection to the FTP server.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the connection was closed successfully |

=== "JSON"

    ```json
    {
        "close_connection": {}
    }
    ```

---

## Frequently Asked Questions

### How do I configure FTP credentials in EasyTask?
Use the EasyTask vault system to securely store your FTP server credentials. Navigate to the integration configuration page and add your FTP server address, port, username, and password under a vault key like `ftp/secret`.

### Can I use FTP with both EasyTask Cloud and On-Premises?
Yes, FTP works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot FTP connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your FTP server address, port, and credentials in the vault, ensure the FTP server is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
