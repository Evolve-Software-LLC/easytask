---
title: HashiCorp Vault - EasyTask Integration Guide
description: Connect HashiCorp Vault with EasyTask for automated secrets management, encryption operations, and secure credential orchestration in scheduled workflows.
keywords:
  - hashicorp vault
  - easytask
  - workflow orchestration
  - automation
  - secrets management
  - encryption
  - vault integration
---

# Vault

HashiCorp Vault is an identity-based secrets and encryption management system. A secret is anything that you want to tightly control access to, such as API encryption keys, passwords, and certificates. Vault provides encryption services that are gated by authentication and authorization methods. Using Vault's UI, CLI, or HTTP API, access to secrets and other sensitive data can be securely stored and managed, tightly controlled (restricted), and auditable.

## Why Integrate HashiCorp Vault with EasyTask?

HashiCorp Vault is the industry standard for secrets management, encryption as a service, and identity-based access control. By integrating Vault with EasyTask, you can automate secret lifecycle management, health checks, and encryption operations on a configurable schedule. EasyTask enables you to read and write secrets, check vault health, manage key-value stores, and orchestrate credential rotation — all triggered by scheduled tasks. This integration is ideal for automating secret rotation, scheduling compliance audits, and building secure CI/CD pipelines without manual credential management.

## Integration Server Vault details

## Vault Integration JSON Format

Before starting, make sure the vault server is up and running and environment variable VAULT_ADDR is set to the API address and VAULT_TOKEN is set to the vault token.

### Authentication Methods

The Vault integration supports two authentication methods:

#### Method 1: Direct Token (Simple)

Provide the vault root token directly in the `init` section. This is simpler but less secure for production use.

#### Method 2: Vault Path Key (Recommended)

Provide `vault_path_key` which references a path in the primary vault where the secondary vault credentials are stored. The credentials in the primary vault should contain:

```json
{
  "vault_url": "http://localhost:8201",
  "vault_token": "YOUR_SECONDARY_VAULT_TOKEN",
  "use_tls": false
}
```

For TLS mode, include:
```json
{
  "vault_url": "https://localhost:8201",
  "vault_token": "YOUR_SECONDARY_VAULT_TOKEN",
  "use_tls": true,
  "ca_cert_path": "/path/to/ca.crt",
  "vault_cert_path": "/path/to/vault.crt",
  "vault_key_path": "/path/to/vault.key"
}
```

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | user | string | User identifier for logging | No |
    | integration | string | Type of integration (must be "vault") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.root_token | string | Root token for Vault authentication (Method 1) | No* |
    | init.vault_path_key | string | Path to vault credentials in primary vault (Method 2) | No* |
    | action | array | List of actions to be performed | Yes |

    *Either `root_token` or `vault_path_key` is required.

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": []
      }
    ]
    ```

## Example cURL Commands

### Sample Usage of Vault

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d '[
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "is_active": {}
          },
          {
            "show_path": {}
          }
        ]
      }
    ]'
    ```

=== "Output"

    ```json
    [{
      "integration": "vault",
      "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
      "init": {
        "vault_path_key": "vault/newtest"
      },
      "error": false,
      "action": [
        {"is_active": true},
        {"show_path": ["cubbyhole/", "identity/", "secret/", "sys/"]}
      ]
    }]
    ```

## Functions

### `initialise`

**Initialisation**:

This function initializes the vault server, creating a file containing the root token and unseal keys.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | shares | integer | Number of parts (shares) the unseal key is divided into (default: 5) | No |
    | threshold | integer | Number of shares required to reconstruct the unseal key (default: 3) | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the initialise action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "initialise": {
              "shares": 5,
              "threshold": 3
            }
          }
        ]
      }
    ]
    ```

### `unseal`

**Unsealing**:

This function unseals the vault server using the provided unseal keys.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | keys | array[string] | List of keys to unseal | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the unseal action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "unseal": {
              "keys": [
                "YOUR_UNSEAL_KEY_1",
                "YOUR_UNSEAL_KEY_2",
                "YOUR_UNSEAL_KEY_3"
              ]
            }
          }
        ]
      }
    ]
    ```

### `seal`

**Sealing**:

This function seals the vault server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the seal action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "seal": {}
          }
        ]
      }
    ]
    ```

### `mount`

**Mount**:

This function enables a new secret engine at the given path.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path for the mount point | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the mount action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "mount": {
              "path": "test_mount"
            }
          }
        ]
      }
    ]
    ```

### `unmount`

**Unmount**:

This function disables a secret engine at the given path.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to unmount | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the unmount action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "unmount": {
              "path": "test_mount"
            }
          }
        ]
      }
    ]
    ```

`Note: Be careful when using the unmount function, as it will delete all the secrets present in the path.`

### `create_secret`

**Writing a secret**:

This function adds a secret to the given path in the vault.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to add the secret | Yes |
    | secret | object | Secret to be added | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_secret action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "create_secret": {
              "path": "secret/test",
              "secret": {
                "username": "admin",
                "password": "YOUR_PASSWORD"
              }
            }
          }
        ]
      }
    ]
    ```

### `read_secret`

**Reading a secret**:

This function retrieves the secret from the given path in the vault.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to view secrets | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the read_secret action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "read_secret": {
              "path": "secret/test"
            }
          }
        ]
      }
    ]
    ```

### `delete_secret`

**Deleting a secret**:

This function deletes a secret at the given path in the vault.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | path | string | Path to delete the secret | Yes |
    | complete | boolean | Whether to delete all secrets in the given path (default: false) | No |
    | secret | string | Specific secret to be deleted in the given path (default: null) | No |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_secret action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "delete_secret": {
              "path": "secret/test",
              "secret": "username"
            }
          }
        ]
      }
    ]
    ```

Note: Be careful when using this function, as the secret once deleted cannot be retrieved again.

### `show_path`

**Displaying all enabled secret engines**:

This function displays all enabled secret engines.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the show_path action |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "show_path": {}
          }
        ]
      }
    ]
    ```

### `is_active`

**Check vault status**:

This function checks if the vault is initialized and unsealed (active).

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | None | - | No parameters required | - |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (vault) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains boolean result (true if vault is active) |

=== "JSON"

    ```json
    [
      {
        "user": "test user",
        "integration": "vault",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
          "vault_path_key": "vault/newtest"
        },
        "action": [
          {
            "is_active": {}
          }
        ]
      }
    ]
    ```

## FAQ

### What HashiCorp Vault operations does EasyTask support?

EasyTask supports Vault operations including reading and writing secrets, checking vault health status (`is_active`), managing key-value stores, and performing secret lifecycle operations. You can automate credential rotation and secrets management through scheduled tasks.

### How does EasyTask authenticate with HashiCorp Vault?

The Vault integration supports two authentication methods: direct token authentication (providing the root token in the init section) and vault path key authentication (referencing credentials stored in the primary vault). TLS mode is also supported for secure communication with certificate-based verification.

### Can I automate secret rotation with EasyTask?

Yes. By combining Vault integration with EasyTask's scheduling engine, you can create tasks that automatically rotate secrets, update credentials across multiple systems, and validate secret freshness on a configurable schedule. This eliminates manual credential management and improves security posture.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
