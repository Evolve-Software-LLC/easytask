---
description: "Integrate Jira with EasyTask for automated issue creation, project data fetching, and streamlined project management in your scheduled workflows."
keywords:
  - Jira automation
  - issue tracking
  - project management scheduling
  - Jira integration
  - automated issue creation
  - EasyTask Jira
---

# Jira API

The Jira API provides a set of operations for interacting with Atlassian Jira, allowing users to manage projects, issues, and fields programmatically.

## Why Integrate Jira with EasyTask?

Jira is the leading project management and issue tracking platform used by teams worldwide. EasyTask enables scheduled tasks to create issues, fetch project data, and automate ticket management seamlessly. This integration is ideal for incident management, release tracking, and automated reporting pipelines -- helping your team stay on top of every issue without manual overhead.

## Required Values in Vault

```
{
   "secret": {
         "api_key": "xxxxxxxx (String Type)",
         "email": "xxxxxxxx (String Type)"
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
        "integration": "jira",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "jira/secret"
        },
        "action": [
            {
                "fetch_all_projects": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
    {
        "fetch_all_projects": [
            {
                "id": "10000",
                "key": "EV",
                "name": "EVOLVE"
            }
        ]
    }
    ```

## Functions

### `fetch_all_projects`

**fetch_all_projects**: This function retrieves all projects in the Jira instance.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing project information |

=== "JSON"

    ```json
    {
        "fetch_all_projects": {}
    }
    ```

### `fetch_all_jira_fields`

**fetch_all_jira_fields**: This function retrieves all available fields in the Jira instance.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of dictionaries containing field information |

=== "JSON"

    ```json
    {
        "fetch_all_jira_fields": {}
    }
    ```

### `fetch_issue_id`

**fetch_issue_id**: This function retrieves the issue ID for a given project.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | project_name | str | Name of the project | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Issue ID for the specified project |

=== "JSON"

    ```json
    {
        "fetch_issue_id": {
            "project_name": "EVOLVE"
        }
    }
    ```

### `create_issue_ticket`

**create_issue_ticket**: This function creates a new issue ticket in Jira.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | data | dict | Dictionary containing issue details | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Details of the created issue |

=== "JSON"

    ```json
    {
        "create_issue_ticket": {
            "data": {
                "project": "EV",
                "summary": "Testing summary",
                "description": "",
                "issuetype": {"name": "Epic"}
            }
        }
    }
    ```

## FAQ

### What Jira operations does EasyTask support?

EasyTask supports fetching all projects, fetching all Jira fields, fetching issue IDs by project, and creating issue tickets. These operations can be used within any scheduled workflow to automate your Jira processes.

### How do I create Jira issues from scheduled tasks?

Use the `create_issue_ticket` action in your workflow configuration. Provide a `data` dictionary containing the project key, summary, description, and issue type. EasyTask will authenticate using credentials stored in your vault and create the issue automatically when the scheduled task runs.

### Can I fetch Jira project data in workflows?

Yes. Use the `fetch_all_projects` action to retrieve a list of all projects, or `fetch_issue_id` to get the issue ID for a specific project. The returned data can be used in subsequent workflow steps for conditional logic or reporting.

## Next Steps

- [Introduction to Integrations](integrations_intro.md)
- [ServiceNow Integration](servicenow.md)
- [Slack Integration](slack.md)
