---
title: Confluence - EasyTask Integration Guide
description: Connect Confluence with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing pages and spaces.
keywords:
  - confluence
  - easytask
  - workflow orchestration
  - automation
  - documentation
  - wiki
---

# Confluence API

The Confluence API provides a set of endpoints for managing pages and spaces within Confluence. It allows users to programmatically create, read, update, and delete content in Confluence.

## Why Integrate Confluence with EasyTask?

Integrating Confluence with EasyTask enables you to automate content and documentation management workflows. This integration allows you to:

- **Automate Page Creation and Updates**: Create and manage Confluence pages automatically as part of your EasyTask workflows, keeping documentation in sync with project changes.
- **Streamline Content Workflows**: Check page existence, retrieve page IDs, and perform content operations without manual intervention through automated orchestration.
- **Support Cloud and On-Premises**: Seamlessly integrate with both Confluence Cloud and Confluence Server deployments using a unified EasyTask configuration approach.

## Required Values in Vault

The Confluence integration supports both **Confluence Cloud** and **Confluence Server** (on-premise).

### Confluence Cloud

```json
{
   "secret": {
         "cloud": true,
         "url": "https://your-instance.atlassian.net/wiki",
         "email": "your-email@example.com",
         "API_token": "your-api-token"
   }
}
```

| Field | Type | Description |
|-------|------|-------------|
| cloud | boolean | Must be `true` for Confluence Cloud |
| url | string | Your Confluence Cloud URL (e.g., `https://xxx.atlassian.net/wiki`) |
| email | string | Your Atlassian account email |
| API_token | string | API token from [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens) |

### Confluence Server (On-Premise)

```json
{
   "secret": {
         "cloud": false,
         "host": "xxxxxxxx (String Type)",
         "port": "xxxxxxxx (String Type)",
         "username": "xxxxxxxxx (String Type)",
         "password": "xxxxxxxx (String Type)"
   }
}
```

| Field | Type | Description |
|-------|------|-------------|
| cloud | boolean | Must be `false` for Confluence Server |
| host | string | Server hostname or IP address |
| port | string | Server port (typically `8090`) |
| username | string | Confluence username |
| password | string | Confluence password |

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
        "integration": "confluence",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "confluence/secret"
        },
        "action": [
            {
                "create_page": {
                    "space": "DEMO",
                    "title": "Sample Page Title",
                    "body": "This is the body of the page."
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    {
        "create_page": {
            "id": "12345678",
            "type": "page",
            "status": "current",
            "title": "Sample Page Title",
            "space": {"key": "DEMO"}
        }
    }
    ```

## Functions

### `create_page`

**create_page**: This function creates a new page in the specified Confluence space.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | space | str | Key of the space where the page will be created | yes |
    | title | str | Title of the new page | yes |
    | body | str | Content of the new page (can include HTML) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Contains details of the created page, including its ID |

=== "JSON"

    ```json
    {
        "create_page": {
            "space": "DEMO",
            "title": "Sample Page Title",
            "body": "This is the body of the page."
        }
    }
    ```

### `check_page_exists`

**check_page_exists**: This function checks if a page with the given title exists in the specified space.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | space | str | Key of the space to check | yes |
    | title | str | Title of the page to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | Returns true if the page exists, false otherwise |

=== "JSON"

    ```json
    {
        "check_page_exists": {
            "space": "DEMO",
            "title": "Sample Page Title"
        }
    }
    ```

### `get_page_id`

**get_page_id**: This function retrieves the ID of a page with the given title in the specified space.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | space | str | Key of the space to search | yes |
    | title | str | Title of the page to find | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | The ID of the page if found, None otherwise |

=== "JSON"

    ```json
    {
        "get_page_id": {
            "space": "DEMO",
            "title": "Sample Page Title"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Confluence credentials in EasyTask?
Use the EasyTask vault system to securely store your Confluence connection credentials. For Confluence Cloud, add your URL, email, and API token. For Confluence Server, add your host, port, username, and password under a vault key like `confluence/secret`.

### Can I use Confluence with both EasyTask Cloud and On-Premises?
Yes, Confluence works seamlessly with both EasyTask Cloud and On-Premises deployments. The integration supports both Confluence Cloud and Confluence Server (on-premise) configurations.

### How do I troubleshoot Confluence connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials (API token for Cloud or username/password for Server) in the vault, ensure the Confluence instance is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)

