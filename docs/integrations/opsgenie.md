---
title: Opsgenie - EasyTask Integration Guide
description: Connect Opsgenie with EasyTask for automated incident and alert management. Step-by-step setup, configuration, and best practices for Opsgenie integration.
keywords:
  - opsgenie
  - easytask
  - workflow orchestration
  - automation
  - incident management
  - alerting
---

# Opsgenie API

The Opsgenie API provides a set of operations for interacting with Opsgenie, allowing users to retrieve account information, create incidents, and create alerts.

## Why Integrate Opsgenie with EasyTask?

Integrating Opsgenie with EasyTask enables you to automate incident management and alerting within your workflows. This integration allows you to:

- **Automate Incident Creation**: Programmatically create and prioritize incidents in Opsgenie as part of your automated monitoring and response workflows.
- **Streamline Alert Management**: Generate alerts with custom priorities and aliases to ensure the right teams are notified at the right time.
- **Centralize API Key Management**: Store Opsgenie API keys and proxy configurations securely in the EasyTask vault for consistent, auditable access.

## Required Values in Vault

```
"secret": {
    "api_key": "YOUR_OPSGENIE_API_KEY",
    "host": "https://api.opsgenie.com",
    "integration_api_key": "YOUR_OPSGENIE_INTEGRATION_API_KEY",
    "proxy_url": "http://10.0.21.254:3128"
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
        "integration": "opsgenie",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "opsgenie/secret"
        },
        "action": [
            {
                "get_account_info": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "opsgenie",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "opsgenie/secret"
        },
        "error": false,
        "action": [
            {"get_account_info": {"data": {"name": "team-ab9jkdt885nu",
        "plan": {"is_yearly": false,
                "max_user_count": 2147483647,
                "name": "Enterprise Trial"},
        "user_count": 1},
        "request_id": "f7de72c2-74f2-487b-88b9-5b2678d97cf7",
        "took": 0.058}}
        ]
    }

    ```

## Functions

### `get_account_info`

**get_account_info**: This function retrieves information about the Opsgenie account.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing account information |

=== "JSON"

    ```json
    {
        "get_account_info": {}
    }
    ```

### `create_incident`

**create_incident**: This function creates a new incident in Opsgenie.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message | str | Description of the incident | yes |
    | priority | str | Priority level of the incident (e.g., "P1") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing details of the created incident |

=== "JSON"

    ```json
    {
        "create_incident": {
            "message": "Something very bad happened!!",
            "priority": "P1"
        }
    }
    ```

### `create_alert`

**create_alert**: This function creates a new alert in Opsgenie.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message | str | Description of the alert | yes |
    | priority | str | Priority level of the alert (e.g., "P1") | yes |
    | alias | str | Unique identifier for the alert | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Dictionary containing details of the created alert |

=== "JSON"

    ```json
    {
        "create_alert": {
            "message": "Something very bad happened!!",
            "priority": "P1",
            "alias": "unique_alert_identifier"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Opsgenie credentials in EasyTask?
Use the EasyTask vault system to securely store your Opsgenie connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `opsgenie/secret`. Include the API key, host URL, integration API key, and proxy URL if needed.

### Can I use Opsgenie with both EasyTask Cloud and On-Premises?
Yes, Opsgenie works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the Opsgenie API endpoint is reachable from the integration server.

### How do I troubleshoot Opsgenie connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your API keys in the vault, ensure the Opsgenie API host is accessible from the integration server, and test connectivity using the built-in connection test feature. If using a proxy, confirm the proxy URL is correct and accessible.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
