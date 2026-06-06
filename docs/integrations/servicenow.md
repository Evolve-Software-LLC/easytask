---
description: ServiceNow integration for automated IT service management, incident creation, and ticket lifecycle management in scheduled workflows.
keywords:
  - ServiceNow automation
  - ITSM scheduling
  - incident management
  - ServiceNow integration
  - ticket lifecycle automation
  - IT service management
---

# Servicenow

ServiceNow is a cloud-based platform that provides IT service management (ITSM) tools. A ServiceNow Integration instance allows you to perform various operations on incident and problem records directly from the platform. The integration requires authentication and proper configuration.

## Why Integrate ServiceNow with EasyTask?

ServiceNow is the leading enterprise platform for IT Service Management (ITSM), enabling organizations to streamline incident, problem, and change management workflows. By integrating ServiceNow with EasyTask, you can leverage scheduled tasks to automatically create, update, and query incidents, problems, and other records on a time-based trigger — no manual intervention required.

This integration is ideal for **incident response automation**, where scheduled workflows can open and escalate tickets the moment monitoring thresholds are breached. It also supports **compliance reporting** by periodically retrieving and archiving ticket data, and **service desk orchestration** by synchronizing ticket states across systems as part of a broader automated pipeline.

Whether you need to auto-create incidents from health checks, keep stakeholders updated on a schedule, or audit your service desk activity, the ServiceNow + EasyTask integration brings powerful, hands-off ITSM automation to your organization.

## Integration Server Vault details

### Creating a ServiceNow Personal Developer Instance

To create a ServiceNow Personal Developer Instance (PDI), follow these steps:

1. Sign up for a ServiceNow Developer account:
   - Visit the ServiceNow Developer site at https://developer.servicenow.com/.
   - Click on the "Sign Up" button and complete the registration process.

2. Request a Personal Developer Instance:
   - Once logged in, navigate to the "Manage" section and select "Instance".
   - Click on "Request Instance".
   - Choose the version of the ServiceNow instance you want to use and click on "Request".

3. Access your PDI:
   - After the instance is ready, you will receive an email with the instance URL, username, and password.
   - Use these credentials to log in to your PDI.

Note: If the PDI is not used for 2 weeks, it will get expired. Make sure to log in periodically to keep it active.

### Required secrets in Vault

=== "JSON"

    ```json
    {
      "secret": {
        "instance": "devxxxxxx",
        "instance_url": "https://devxxxxxx.service-now.com",
        "password": "xxxxxxxxx",
        "username": "xxxxxxxxx"
      }
    }
    ```

### ServiceNow Integrations JSON Format

=== "Table"

    | Field | Type | Description | Required |
    |-------|------|-------------|----------|
    | is_credentials | object | Credentials for authentication | Yes |
    | is_credentials.userid | string | User ID for authentication | Yes |
    | is_credentials.passwd | string | Password for authentication | Yes |
    | integrations | array | List of integration objects | Yes |
    | integration | string | Type of integration (must be "servicenow") | Yes |
    | uuid | string | Unique identifier for the integration instance | Yes |
    | init | object | Initialization parameters | Yes |
    | init.vault_path_key | string | Path to the vault containing ServiceNow credentials | Yes |
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
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of Servicenow 

=== "Input Command"

    ```sh
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d'
      {
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [{
            "integration": "servicenow",
            "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
            "init": {
                "vault_path_key": "servicenow/server1"
            },
            "action": [
                {
                    "create_new_record":{
                        "record_details":{
                            "short_description":"Created from slurpper",
                            "description": "Slurpper"
                        }
                    }
                },
            ]
        }]
      }'

    ```

=== "Output"

    ```json
    {
        {
          "create_new_record": "INC0010049"
        }
    }
    ```

## Functions

### `get_ticket_details`

**Get Incident Ticket Details**:

This function retrieves all the ticket details by providing a ticket number.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | ticket_number | string | Unique identifier assigned to each incident record | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_ticket_details action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "get_ticket_details": {
                "ticket_number": "INC0010052"
              }
            }
          ]
        }
      ]
    }
    ```

### `create_new_record`

**Create New Incident Record**:

This function creates a new record in an incident table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | record_details | object | Record details required to document, categorize, and manage an incident | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_new_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "create_new_record": {
                "record_details": {
                  "short_description": "Created from slurpper",
                  "description": "Slurpper"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `update_record`

**Update Incident Record**:

This function updates a record with the incident number and dictionary of updated details provided.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | incident_number | string | Unique identifier assigned to each incident record | Yes |
    | up_record | object | Details to be updated | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "update_record": {
                "incident_number": "INC0010052",
                "up_record": {
                  "short_description": "Updated Test Incident short description",
                  "state": 5
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_record`

**Delete Incident Record**:

This function deletes an incident record from the incident table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | incident_number | string | Unique identifier assigned to each incident record | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "delete_record": {
                "incident_number": "INC0010052"
              }
            }
          ]
        }
      ]
    }
    ```

### `retrieve_ticket_with_daterange`

**Retrieve Incident Ticket with Date Range**:

This function fetches all ticket details that start with a certain incident number and are within a specified date range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | incident_number | string | Unique identifier assigned to each incident record | Yes |
    | days | integer | Number of days to look back from today | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the retrieve_ticket_with_daterange action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "retrieve_ticket_with_daterange": {
                "incident_number": "INC",
                "days": 15
              }
            }
          ]
        }
      ]
    }
    ```

### `get_problem_ticket_details`

**Get Problem Ticket Details**:

This function retrieves all problem table details by providing a ticket number.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | ticket_number | string | Unique identifier assigned to each problem record | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_problem_ticket_details action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "get_problem_ticket_details": {
                "ticket_number": "INC0010033"
              }
            }
          ]
        }
      ]
    }
    ```

### `create_new_problem_record`

**Create New Problem Record**:

This function creates a new record in the problem table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | problem_details | object | Details of the Problem record to be added | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_new_problem_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "create_new_problem_record": {
                "problem_details": {
                  "short_description": "Pysnow created incident",
                  "description": "This is awesome"
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `update_problem_record`

**Update Problem Record**:

This function updates a problem record with the provided ticket number and updated details.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | ticket_number | string | Unique identifier assigned to each problem record | Yes |
    | up_record | object | Details of Problem record to be updated | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_problem_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "update_problem_record": {
                "ticket_number": "PRB0040043",
                "up_record": {
                  "short_description": "Test case updated short description",
                  "state": 5
                }
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_problem_record`

**Delete Problem Record**:

This function deletes a problem record from the problem table.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | ticket_number | string | Unique identifier assigned to each problem record | Yes |

=== "Output"

    | Key | Type | Description |
    |-----|------|-------------|
    | integration | string | The type of integration used (servicenow) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_problem_record action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "servicenow",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "servicenow/server1"
          },
          "action": [
            {
              "delete_problem_record": {
                "ticket_number": "PRB0040043"
              }
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What ServiceNow operations does EasyTask support?

EasyTask supports the following ServiceNow operations for both **incident** and **problem** records:

- **Get ticket details** — Retrieve full details of an incident or problem by ticket number.
- **Create new record** — Create new incident or problem records with custom fields.
- **Update record** — Modify existing incident or problem records by ticket number.
- **Delete record** — Remove incident or problem records from the table.
- **Retrieve tickets by date range** — Query incident records matching a prefix within a lookback window.

### How do I create ServiceNow incidents from scheduled tasks?

To create incidents from a scheduled task, configure a ServiceNow integration instance in your task definition. Provide the vault path for your ServiceNow credentials and use the `create_new_record` action with the desired `record_details` (such as `short_description` and `description`). When the scheduled task runs, EasyTask will authenticate with ServiceNow and create the incident automatically.

### Can I query ServiceNow records by date range?

Yes. Use the `retrieve_ticket_with_daterange` action. Specify an `incident_number` prefix (e.g., `"INC"` to match all incidents) and a `days` value indicating how many days to look back. EasyTask will return all matching records created within that time window.

## Next Steps

- [Integrations Overview](integrations_intro.md) — Explore all available integrations in EasyTask.
- [Jira Integration](jira.md) — Automate issue tracking and project management with Jira.
- [Datadog Integration](datadogs.md) — Connect Datadog monitoring to your scheduled workflows.
