---
title: Nagios - EasyTask Integration Guide
description: Connect Nagios with EasyTask for automated monitoring and alert management. Step-by-step setup, configuration, and best practices for Nagios integration.
keywords:
  - nagios
  - easytask
  - workflow orchestration
  - automation
  - monitoring
  - alert management
---

# Nagios API

The Nagios API provides a set of endpoints for retrieving information about hosts, services, and other objects monitored by Nagios. It allows users to access historical data, current status, and configuration details.

## Why Integrate Nagios with EasyTask?

Integrating Nagios with EasyTask enables you to automate infrastructure monitoring and incident response workflows. This integration allows you to:

- **Automate Alert Retrieval**: Programmatically query archived alerts, notifications, and state changes to feed into automated incident response pipelines.
- **Streamline Infrastructure Visibility**: Retrieve host, service, and contact information in real time to power automated health checks and reporting.
- **Orchestrate Monitoring Workflows**: Combine Nagios monitoring data with other integrations to create end-to-end observability and remediation workflows.

## Required Values in Vault

```
{

    "secret": {
           "host": "xx.x.xx.xxx",
           "port": "xxxx",
           "password" : "xxxxxx",
           "username" : "xxxxx"
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
        "integration": "nagios",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "nagios/secret"
        },
        "action": [
            {
                "archive_alert_list": {
                    "starttime": 2000,
                    "endtime": 2300
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "nagios",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
                    "vault_path_key": "nagios/server1"
        },
        "error": false,
        "action": [
            {"archive_alert_list": {
                        "data":
                                {
                                    "alertlist": [],
                                    "selectors": {
                                    "endtime": 2300000,
                                    "starttime": 2000000}
                                    },
                                    "format_version": 0,
                                    "result":
                                        {
                                            "cgi": "archivejson.cgi",
                                            "last_data_update": 0,
                                            "message": "",
                                            "program_start": 1716287608000,
                                            "query": "alertlist",
                                            "query_status": "released",
                                            "query_time": 1716483836000,
                                            "type_code": 0,
                                            "type_text": "Success",
                                            "user": "nagiosadmin"
                                            }
                                        }
                                }
        ]
    }

    ```

## Functions

### `archive_alert_list`

**archive_alert_list**: This function retrieves a list of alerts within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the alert list (UNIX timestamp) | yes |
    | endtime | int | End time for the alert list (UNIX timestamp) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of alerts within the specified time range |

=== "JSON"

    ```json
    {
        "archive_alert_list": {
            "starttime": 2000,
            "endtime": 2300
        }
    }
    ```

### `archive_alert_count`

**archive_alert_count**: This function retrieves the count of alerts within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the alert count (UNIX timestamp) | yes |
    | endtime | int | End time for the alert count (UNIX timestamp) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of alerts within the specified time range |

=== "JSON"

    ```json
    {
        "archive_alert_count": {
            "starttime": 2000,
            "endtime": 2300
        }
    }
    ```

### `archive_notification_count`

**archive_notification_count**: This function retrieves the count of notifications within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the notification count (UNIX timestamp) | yes |
    | endtime | int | End time for the notification count (UNIX timestamp) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of notifications within the specified time range |

=== "JSON"

    ```json
    {
        "archive_notification_count": {
            "starttime": 2000,
            "endtime": 2300
        }
    }
    ```

### `archive_notification_list`

**archive_notification_list**: This function retrieves a list of notifications within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the notification list (UNIX timestamp) | yes |
    | endtime | int | End time for the notification list (UNIX timestamp) | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of notifications within the specified time range |

=== "JSON"

    ```json
    {
        "archive_notification_list": {
            "starttime": 2000,
            "endtime": 2300
        }
    }
    ```

### `archive_state_change_list`

**archive_state_change_list**: This function retrieves a list of state changes for a specific object type within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the state change list (UNIX timestamp) | yes |
    | endtime | int | End time for the state change list (UNIX timestamp) | yes |
    | objecttype | str | Type of object (e.g., "host" or "service") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of state changes within the specified time range |

=== "JSON"

    ```json
    {
        "archive_state_change_list": {
            "starttime": 2000,
            "endtime": 2300,
            "objecttype": "host"
        }
    }
    ```

### `archive_availability`

**archive_availability**: This function retrieves availability information for a specific object type within a specified time range.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | starttime | int | Start time for the availability data (UNIX timestamp) | yes |
    | endtime | int | End time for the availability data (UNIX timestamp) | yes |
    | availabilityobjecttype | str | Type of object for availability data (e.g., "hosts" or "services") | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Availability information for the specified object type |

=== "JSON"

    ```json
    {
        "archive_availability": {
            "starttime": 2000,
            "endtime": 2300,
            "availabilityobjecttype": "hosts"
        }
    }
    ```

### `object_host`

**object_host**: This function retrieves information about a specific host.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | hostname | str | Name of the host | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the specified host |

=== "JSON"

    ```json
    {
        "object_host": {
            "hostname": "localhost"
        }
    }
    ```

### `object_hostlist`

**object_hostlist**: This function retrieves a list of all hosts.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all hosts |

=== "JSON"

    ```json
    {
        "object_hostlist": {}
    }
    ```

### `object_hostcount`

**object_hostcount**: This function retrieves the count of all hosts.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all hosts |

=== "JSON"

    ```json
    {
        "object_hostcount": {}
    }
    ```

### `object_hostgroup`

**object_hostgroup**: This function retrieves information about a specific host group.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | hostgroup | str | Name of the host group | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the specified host group |

=== "JSON"

    ```json
    {
        "object_hostgroup": {
            "hostgroup": "linux-servers"
        }
    }
    ```

### `object_hostgrouplist`

**object_hostgrouplist**: This function retrieves a list of all host groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all host groups |

=== "JSON"

    ```json
    {
        "object_hostgrouplist": {}
    }
    ```

### `object_hostgroupcount`

**object_hostgroupcount**: This function retrieves the count of all host groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all host groups |

=== "JSON"

    ```json
    {
        "object_hostgroupcount": {}
    }
    ```

### `object_service`

**object_service**: This function retrieves information about a specific service.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | hostname | str | Name of the host | yes |
    | servicedescription | str | Description of the service | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the specified service |

=== "JSON"

    ```json
    {
        "object_service": {
            "hostname": "localhost",
            "servicedescription": "HTTP"
        }
    }
    ```

### `object_servicelist`

**object_servicelist**: This function retrieves a list of all services.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all services |

=== "JSON"

    ```json
    {
        "object_servicelist": {}
    }
    ```

### `object_servicecount`

**object_servicecount**: This function retrieves the count of all services.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all services |

=== "JSON"

    ```json
    {
        "object_servicecount": {}
    }
    ```

### `object_servicegrouplist`

**object_servicegrouplist**: This function retrieves a list of all service groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all service groups |

=== "JSON"

    ```json
    {
        "object_servicegrouplist": {}
    }
    ```

### `object_servicegroupcount`

**object_servicegroupcount**: This function retrieves the count of all service groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all service groups |

=== "JSON"

    ```json
    {
        "object_servicegroupcount": {}
    }
    ```

### `object_contactlist`

**object_contactlist**: This function retrieves a list of all contacts.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all contacts |

=== "JSON"

    ```json
    {
        "object_contactlist": {}
    }
    ```

### `object_contactcount`

**object_contactcount**: This function retrieves the count of all contacts.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all contacts |

=== "JSON"

    ```json
    {
        "object_contactcount": {}
    }
    ```

### `object_contactgroup`

**object_contactgroup**: This function retrieves information about a specific contact group.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | contactgroup | str | Name of the contact group | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the specified contact group |

=== "JSON"

    ```json
    {
        "object_contactgroup": {
            "contactgroup": "admins"
        }
    }
    ```

### `object_contactgroupcount`

**object_contactgroupcount**: This function retrieves the count of all contact groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all contact groups |

=== "JSON"

    ```json
    {
        "object_contactgroupcount": {}
    }
    ```

### `object_contactgrouplist`

**object_contactgrouplist**: This function retrieves a list of all contact groups.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all contact groups |

=== "JSON"

    ```json
    {
        "object_contactgrouplist": {}
    }
    ```

### `object_timeperiod`

**object_timeperiod**: This function retrieves information about a specific time period.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | timeperiod | str | Name of the time period | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the specified time period |

=== "JSON"

    ```json
    {
        "object_timeperiod": {
            "timeperiod": "24x7"
        }
    }
    ```

### `object_timeperiodcount`

**object_timeperiodcount**: This function retrieves the count of all time periods.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Count of all time periods |

=== "JSON"

    ```json
    {
        "object_timeperiodcount": {}
    }
    ```

### `object_timeperiodlist`

**object_timeperiodlist**: This function retrieves a list of all time periods.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of all time periods |

---

## Frequently Asked Questions

### How do I configure Nagios credentials in EasyTask?
Use the EasyTask vault system to securely store your Nagios connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `nagios/server1`. Include the host, port, username, and password for your Nagios instance.

### Can I use Nagios with both EasyTask Cloud and On-Premises?
Yes, Nagios works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical — just ensure the Nagios server is reachable from the integration server.

### How do I troubleshoot Nagios connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials in the vault, ensure the Nagios server is accessible from the integration server, and test connectivity using the built-in connection test feature. Confirm the Nagios CGI endpoint is properly configured.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
