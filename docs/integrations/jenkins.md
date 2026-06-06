---
description: Jenkins integration for EasyTask enables CI/CD pipeline automation, job management, and build triggering from scheduled tasks.
keywords:
  - Jenkins CI/CD automation
  - build scheduling
  - pipeline orchestration
  - Jenkins integration
  - EasyTask Jenkins
---

# Jenkins Integrations

Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration, and continuous delivery.

## Why Integrate Jenkins with EasyTask?

Jenkins is the most widely used CI/CD automation server in the world, trusted by teams of all sizes to manage their build, test, and deployment pipelines. By integrating Jenkins with EasyTask, you unlock powerful automation capabilities that go beyond what Jenkins can do alone:

- **Trigger Builds from Scheduled Tasks** — Use EasyTask's scheduling engine to kick off Jenkins builds on a cron-like schedule, eliminating the need for manual triggers or Jenkins-native cron configurations.
- **Manage Jobs and Views** — Create, copy, enable, disable, and delete Jenkins jobs and views directly through EasyTask actions, centralizing your CI/CD management.
- **Monitor Build Status** — Retrieve build information, queued jobs, node health, and plugin status as part of your automated workflows.
- **Orchestrate Complete CI/CD Pipelines** — Chain Jenkins operations with other integrations (Slack notifications, GitHub webhooks, etc.) to build end-to-end delivery pipelines.

This integration is perfect for **release automation**, **nightly builds**, and **deployment orchestration** — any scenario where you need Jenkins to work as part of a larger, scheduled, automated workflow.

## Jenkins Integrations Vault Details

### Required secrets in Vault

=== "Table"

    | Key | Description |
    |-----|-------------|
    | pwd | The password for Jenkins authentication |
    | url | The URL of the Jenkins server |
    | username | The username for Jenkins authentication |

=== "JSON"

    ```json
    {
      "secret": {
        "pwd": "xxxxxxxxxxxxxxx",
        "url": "xxxxxxxxxxxxxxx",
        "username": "xxxxxxxxxxxxxxx"
      }
    }
    ```

### Jenkins Integration JSON Format

=== "Table"

    | Key | Description |
    |-----|-------------|
    | is_credentials | Object containing user credentials |
    | integrations | Array of integration objects |
    | integration | Type of integration (jenkinsintegration in this case) |
    | uuid | Unique identifier for the integration instance |
    | init | Initialization parameters |
    | vault_path_key | Path to the vault containing Jenkins credentials |
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
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": []
        }
      ]
    }
    ```

## Example cURL Commands

### Sample Usage of Jenkins

=== "Input"

    ```json
    curl -X POST http://localhost:8008/run-integration \
    -H "Content-Type: application/json" \
    -d '{
        "is_credentials": {
            "userid": "test",
            "passwd": "test123"
        },
        "integrations": [
            {
                "integration": "jenkinsintegration",
                "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
                "init": {
                    "vault_path_key": "jenkins/server1"
                },
                "action": [
                    {
                        "delete_view": {
                            "view_name": "my_view"
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
        "delete_view": null
    }
    ```

## Function of Jenkins

#### `create_view`

**Create a Jenkins view**:

This function creates a new view in Jenkins. Jenkins views organize and manage jobs within the Jenkins continuous integration/continuous delivery (CI/CD) system. They allow users to group jobs based on specific criteria, enhancing project visibility and workflow management. Views can be customized with filters and dashboards, aiding in efficient monitoring and control of build pipelines.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | view_name | string | The name of the view to be created | Yes |
    | config_xml | string | XML configuration for the Jenkins view | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_view action (null if successful) |

=== "JSON"

    ```json
    {
           "is_credentials": {
             "userid": "test",
             "passwd": "test123"
           },
           "integrations": [
             {
               "integration": "jenkinsintegration",
               "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
               "init": {
                 "vault_path_key": "jenkins/server1"
               },
               "action": [
                 {
                   "create_view": {
                     "view_name": "my_view",
                     "config_xml": "<?xml version='\''1.0'\'' encoding='\''UTF-8'\''?>\n<hudson.model.ListView>\n\t<name>EMPTY</name>\n\t<filterExecutors>false</filterExecutors>\n\t<filterQueue>false</filterQueue>\n\t<properties class='\''hudson.model.View$PropertyList'\''/>\n\t<jobNames>\n\t\t<comparator class='\''hudson.util.CaseInsensitiveComparator'\''/>\n\t</jobNames>\n\t<jobFilters/>\n\t<columns>\n\t\t<hudson.views.StatusColumn/>\n\t\t<hudson.views.WeatherColumn/>\n\t\t<hudson.views.JobColumn/>\n\t\t<hudson.views.LastSuccessColumn/>\n\t\t<hudson.views.LastFailureColumn/>\n\t\t<hudson.views.LastDurationColumn/>\n\t\t<hudson.views.BuildButtonColumn/>\n\t</columns>\n</hudson.model.ListView>"
                   }
                 }
               ]
             }
           ]
    }
    ```

### `delete_view`

**Delete a Jenkins view**:

This function deletes an existing view in Jenkins. It removes the specified view from the Jenkins interface, which can help in organizing and managing the Jenkins dashboard by removing unnecessary or outdated views.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | view_name | string | The name of the view to be deleted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_view action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "delete_view": {
                "view_name": "my_view"
              }
            }
          ]
        }
      ]
    }
    ```

### `update_view_config`

**Update configuration of view**:

This function updates the configuration of an existing Jenkins view. It allows modification of the view's settings and properties by providing a new XML configuration.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | view_name | string | The name of the view to be updated | Yes |
    | config_xml | string | New XML configuration for the Jenkins view | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_view_config action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "update_view_config": {
                "view_name": "my_view",
                "config_xml": "<?xml version='\''1.0'\'' encoding='\''UTF-8'\''?>\n<hudson.model.ListView>\n\t<name>EMPTY</name>\n\t<filterExecutors>false</filterExecutors>\n\t<filterQueue>false</filterQueue>\n\t<properties class='\''hudson.model.View$PropertyList'\''/>\n\t<jobNames>\n\t\t<comparator class='\''hudson.util.CaseInsensitiveComparator'\''/>\n\t</jobNames>\n\t<jobFilters/>\n\t<columns>\n\t\t<hudson.views.StatusColumn/>\n\t\t<hudson.views.WeatherColumn/>\n\t\t<hudson.views.JobColumn/>\n\t\t<hudson.views.LastSuccessColumn/>\n\t\t<hudson.views.LastFailureColumn/>\n\t\t<hudson.views.LastDurationColumn/>\n\t\t<hudson.views.BuildButtonColumn/>\n\t</columns>\n</hudson.model.ListView>"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_view_config`

**Get configuration of Jenkins view**:

This function retrieves the XML configuration of an existing Jenkins view. It allows users to inspect the current settings and properties of a specified view.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | view_name | string | The name of the view to retrieve the configuration for | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_view_config action (XML configuration string) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_view_config": {
                "view_name": "my_view"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_all_views`

**Get all views**:

This function retrieves a list of all the Jenkins views. It provides an overview of all available views in the Jenkins instance, including their class types, names, and URLs.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | get_all_views | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_all_views action |

    Each view in the result contains:
    
    | Field | Type | Description |
    |-------|------|-------------|
    | _class | string | Class name of the Jenkins view |
    | name | string | The name of the Jenkins view |
    | url | string | URL to the Jenkins view |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_all_views": {}
            }
          ]
        }
      ]
    }
    ```

### `get_node_info`

**Get the node information**:

This function retrieves detailed information about a specific Jenkins node (agent). A Jenkins node is a machine that runs jobs dispatched by the Jenkins master, enabling distributed builds and scalability in continuous integration/continuous delivery (CI/CD) processes.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | node_name | string | The name of the node to retrieve information for | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_node_info action |

    The `get_node_info` result is an object with the following structure:

    | Field | Type | Description |
    |-------|------|-------------|
    | _class | string | The Java class name of the node (e.g., "hudson.model.Hudson$MasterComputer") |
    | actions | array | List of actions associated with the node |
    | assignedLabels | array | Labels assigned to the node, each containing a "name" field |
    | ... | ... | Additional fields providing detailed node information |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_node_info": {
                "node_name": "Built-In Node"
              }
            }
          ]
        }
      ]
    }
    ```

Note: The actual node information returned may include many more fields depending on the Jenkins configuration and the specific node. The example output shows a truncated version of the response.

### `check_node_exists`

**Check whether a node exists**:

This function checks if a specified Jenkins node exists in the system.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | node_name | string | The name of the node to check | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the check_node_exists action |

    The `check_node_exists` result is a boolean value:

    | Field | Type | Description |
    |-------|------|-------------|
    | check_node_exists | boolean | true if the node exists, false otherwise |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "check_node_exists": {
                "node_name": "Built-In Node"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_all_nodes`

**Get all the nodes**:

This function retrieves information about all existing Jenkins nodes.

=== "Input Parameters"

    This function does not require any specific input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_all_nodes action |

    The `get_all_nodes` result is an array of node objects:

    | Field | Type | Description |
    |-------|------|-------------|
    | name | string | Name of the node |
    | offline | boolean | Indicates whether the node is offline (true) or online (false) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_all_nodes": {}
            }
          ]
        }
      ]
    }
    ```

### `get_all_plugins_info`

**Get information of all installed plugins**:

This function retrieves information about all installed Jenkins plugins. Jenkins plugins extend functionality, offering integrations with tools and services. They enable custom build steps, reporting, source control integration, and more, enhancing the Jenkins CI/CD pipeline capabilities.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | get_all_plugins_info | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_all_plugins_info action |

    The `get_all_plugins_info` result is an object containing plugin information:

    | Field | Type | Description |
    |-------|------|-------------|
    | (plugin_name, Plugin Long Name) | object | Object containing detailed information about each plugin |

    Each plugin object contains:

    | Field | Type | Description |
    |-------|------|-------------|
    | active | boolean | Indicates if the plugin is active |
    | backupVersion | string | Version of the backup (if any) |
    | bundled | boolean | Indicates if the plugin is bundled with Jenkins |
    | deleted | boolean | Indicates if the plugin is marked for deletion |
    | dependencies | array | List of plugin dependencies |
    | detached | boolean | Indicates if the plugin is detached |
    | downgradable | boolean | Indicates if the plugin can be downgraded |
    | enabled | boolean | Indicates if the plugin is enabled |
    | hasUpdate | boolean | Indicates if an update is available |
    | longName | string | Full name of the plugin |
    | pinned | boolean | Indicates if the plugin is pinned to a specific version |
    | requiredCoreVersion | string | Minimum required Jenkins core version |
    | shortName | string | Short name of the plugin |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_all_plugins_info": {}
            }
          ]
        }
      ]
    }
    ```

### `get_plugin_info`

**Get the Jenkins plugin information**:

This function retrieves detailed information about a specified Jenkins plugin. Plugins are crucial components that extend Jenkins' functionality, enabling custom integrations, build steps, and more.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | plugin_name | string | The name of the plugin to retrieve information for | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_plugin_info action |

    The `get_plugin_info` result is an object with the following structure:

    | Field | Type | Description |
    |-------|------|-------------|
    | active | boolean | Indicates if the plugin is currently active |
    | dependencies | array | List of plugin dependencies, each containing 'optional', 'shortName', and 'version' |
    | detached | boolean | Indicates if the plugin is detached from its original source |
    | downgradable | boolean | Indicates if the plugin can be downgraded |
    | ... | ... | Additional fields providing detailed plugin information |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_plugin_info": {
                "plugin_name": "github"
              }
            }
          ]
        }
      ]
    }
    ```

### `create_job`

**Create a new job**:

This function creates a new Jenkins job. A Jenkins job automates tasks like building, testing, and deploying software. Configured with specific parameters and triggers, jobs streamline CI/CD processes, ensuring consistent and efficient project workflows.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to be created | Yes |
    | config_xml | string | XML configuration for the job | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the create_job action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "create_job": {
                "job_name": "test_job",
                "config_xml": "<?xml version='\''1.0'\'' encoding='\''UTF-8'\''?>\n<project>\n\t<keepDependencies>false</keepDependencies>\n\t<properties/>\n\t<scm class='\''jenkins.scm.NullSCM'\''/>\n\t<canRoam>true</canRoam>\n\t<disabled>false</disabled>\n\t<blockBuildWhenUpstreamBuilding>false</blockBuildWhenUpstreamBuilding>\n\t<triggers class='\''vector'\''/>\n\t<concurrentBuild>false</concurrentBuild>\n\t<builders/>\n\t<publishers/>\n\t<buildWrappers/>\n</project>"
              }
            }
          ]
        }
      ]
    }
    ```

### `copy_job`

**Copy a Jenkins job**:

This function creates a copy of an existing Jenkins job with a new name. This is useful for creating similar jobs or for backup purposes.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | source_job_name | string | The name of the source job to be copied | Yes |
    | dest_job_name | string | The name of the destination (new) job | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the copy_job action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "copy_job": {
                "source_job_name": "test_job",
                "dest_job_name": "test_job_copy"
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_job`

**Delete the specified Jenkins job permanently**:

This function permanently deletes a specified Jenkins job. This action cannot be undone, so it should be used with caution.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to be deleted | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the delete_job action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "delete_job": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `enable_job`

**Enable a Jenkins job**:

This function enables a specified Jenkins job, allowing it to be executed according to its configured triggers or manual runs.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to be enabled | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the enable_job action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "enable_job": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `disable_job`

**Disable a Jenkins job**:

This function disables a specified Jenkins job, preventing it from being executed automatically or manually until it is re-enabled.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to be disabled | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the disable_job action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "disable_job": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `check_job_exists`

**Check whether a Jenkins job exists**:

This function checks if a specified Jenkins job exists in the system.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to check | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the check_job_exists action |

    The `check_job_exists` result is a boolean value:

    | Field | Type | Description |
    |-------|------|-------------|
    | check_job_exists | boolean | true if the job exists, false otherwise |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "check_job_exists": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `num_of_jobs`

**Get number of jobs on Jenkins server**:

This function retrieves the total count of existing jobs on the Jenkins server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | num_of_jobs | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the num_of_jobs action |

    The `num_of_jobs` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | num_of_jobs | integer | The total number of jobs on the Jenkins server |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "num_of_jobs": {}
            }
          ]
        }
      ]
    }
    ```

### `get_job_config`

**Get the configuration of Jenkins job in XML format**:

This function retrieves the XML configuration of a specified Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to retrieve the configuration for | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_job_config action |

    The `get_job_config` result is a string:

    | Field | Type | Description |
    |-------|------|-------------|
    | get_job_config | string | XML configuration of the Jenkins job |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_job_config": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `update_job_name`

**Rename a Jenkins job**:

This function updates the name of an existing Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | cur_job_name | string | The current name of the job | Yes |
    | new_job_name | string | The new name for the job | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_job_name action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "update_job_name": {
                "cur_job_name": "test_job",
                "new_job_name": "test_job_copy_updated"
              }
            }
          ]
        }
      ]
    }
    ```

### `update_job_config`

**Update the configuration of existing Jenkins job**:

This function updates the XML configuration of an existing Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to be updated | Yes |
    | config_xml | string | The new XML configuration of the job | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the update_job_config action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "update_job_config": {
                "job_name": "test_job",
                "config_xml": "<?xml version='\''1.0'\'' encoding='\''UTF-8'\''?>\n<project>\n\t<keepDependencies>false</keepDependencies>\n\t<properties/>\n\t<scm class='\''jenkins.scm.NullSCM'\''/>\n\t<canRoam>true</canRoam>\n\t<disabled>false</disabled>\n\t<blockBuildWhenUpstreamBuilding>false</blockBuildWhenUpstreamBuilding>\n\t<triggers class='\''vector'\''/>\n\t<concurrentBuild>false</concurrentBuild>\n\t<builders/>\n\t<publishers/>\n\t<buildWrappers/>\n</project>"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_job_info`

**Get the Jenkins job information**:

This function retrieves detailed information about a specified Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to retrieve information for | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_job_info action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_job_info": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_all_jobs`

**Get list of all jobs**:

This function retrieves information about all Jenkins jobs on the server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | get_all_jobs | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_all_jobs action |

    Each job in the result contains:

    | Field | Type | Description |
    |-------|------|-------------|
    | _class | string | Class name of the job |
    | name | string | Job name |
    | url | string | URL to the job |
    | color | string | Color of the job (indicating its status) |
    | fullname | string | Full name of the job |

=== "JSON"

    ```json
     {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_all_jobs": {}
            }
          ]
        }
      ]
    }
    ```

### `wipeout_job_workspace`

**Wipe out workspace for the specified Jenkins job**:

This function wipes out the workspace of a specified Jenkins job. A Jenkins job workspace is a directory on the Jenkins server where the job's files are checked out, built, and tested. It contains source code, build artifacts, and logs, providing an isolated environment for job execution.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job whose workspace will be wiped out | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the wipeout_job_workspace action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "wipeout_job_workspace": {
                "job_name": "test_job"
              }
            }
          ]
        }
      ]
    }
    ```

### `start_build`

**Start build on the specified Jenkins job**:

This function starts a build on a specified Jenkins job. A Jenkins job build is an execution instance of a job, performing tasks like compiling code, running tests, and generating artifacts. Each build is uniquely numbered and logged, allowing for tracking, debugging, and analyzing the job's performance and results.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job to start the build on | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the start_build action |

    The `start_build` result is an integer:

    | Field | Type | Description |
    |-------|------|-------------|
    | start_build | integer | The build number acting as a temporary build ID |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "start_build": {
                "job_name": "test_job_copy_updated"
              }
            }
          ]
        }
      ]
    }
    ```

### `get_queue_item`

**Get a specific queue item with queue number**:

This function retrieves information about a specific build instance from the Jenkins queue using the build number. The Jenkins queue holds build tasks waiting to be executed. When jobs are triggered but resources are unavailable, they are placed in the queue. The queue ensures orderly job processing based on priority and availability of executors.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | build_num | integer | Build ID received on instance creation | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_queue_item action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_queue_item": 712
            }
          ]
        }
      ]
}
    ```

### `get_build_info`

**Get the specified build information associated to job with build number**:

This function fetches detailed build information for a specified Jenkins job and build number.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job | Yes |
    | build_num | integer | The build number from the queue | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_build_info action |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_build_info": {
                "job_name": "test_job_copy_updated",
                "build_num": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `get_build_env_vars`

**Get the build environment variables**:

This function retrieves the environment variables for a specific build of a Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job | Yes |
    | build_num | integer | Build number from the queue | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_build_env_vars action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_build_env_vars": {
                "job_name": "test_job_copy_updated",
                "build_num": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `get_running_builds`

**Get a list of all the running builds**:

This function retrieves information about all currently running builds on the Jenkins server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | get_running_builds | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_running_builds action (empty list if no running builds) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_running_builds": {}
            }
          ]
        }
      ]
    }
    ```

### `stop_build`

**Stop the build process of a specific jenkins job**:

This function stops a running build for a specified Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job | Yes |
    | build_num | integer | Build number from the queue | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | action | array | Contains the result of the stop_build action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "stop_build": {
                "job_name": "test_job_copy_updated",
                "build_num": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `delete_build`

**Delete the build process of a specific jenkins job**:

This function deletes a specific build for a Jenkins job.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | job_name | string | The name of the job | Yes |
    | build_num | integer | Build number from the queue | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | action | array | Contains the result of the delete_build action (null if successful) |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "delete_build": {
                "job_name": "test_job_copy_updated",
                "build_num": 1
              }
            }
          ]
        }
      ]
    }
    ```

### `get_queued_job_list`

**Get List of dictionary of jobs**:

This function retrieves a list of all queued jobs on the Jenkins server.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |-----------------|------|-------------|-----------|
    | get_queued_job_list | object | An empty object to trigger the action | Yes |

=== "Output"

    | Output Parameter | Type | Description |
    |------------------|------|-------------|
    | integration | string | The type of integration used (jenkinsintegration) |
    | uuid | string | Unique identifier for the integration instance |
    | init | object | Initialization parameters, including vault path key |
    | error | boolean | Indicates whether an error occurred during the operation |
    | action | array | Contains the result of the get_queued_job_list action |

    Each job in the result contains:

    | Field | Type | Description |
    |-------|------|-------------|
    | _class | string | Class name of the queued item |
    | actions | array | List of actions associated with the queued item |
    | blocked | boolean | Indicates if the item is blocked |
    | buildable | boolean | Indicates if the item is buildable |
    | id | integer | Unique identifier for the queued item |
    | ... | ... | Additional fields providing detailed information about the queued item |

=== "JSON"

    ```json
    {
      "is_credentials": {
        "userid": "test",
        "passwd": "test123"
      },
      "integrations": [
        {
          "integration": "jenkinsintegration",
          "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
          "init": {
            "vault_path_key": "jenkins/server1"
          },
          "action": [
            {
              "get_queued_job_list": {}
            }
          ]
        }
      ]
    }
    ```

## FAQ

### What Jenkins operations does EasyTask support?

EasyTask supports a comprehensive set of Jenkins operations including creating, copying, deleting, enabling, and disabling jobs; building jobs with parameters; creating, updating, and deleting views; retrieving build info, job info, node info, and plugin info; checking job and node existence; managing build queues; and more. Each operation is accessible as an action within an EasyTask integration configuration.

### How do I trigger Jenkins builds from scheduled tasks?

To trigger a Jenkins build from a scheduled task, configure a Jenkins integration in your EasyTask task definition. Set the `integration` type to `jenkinsintegration`, provide the vault path key for your Jenkins credentials, and add a `build_job` action with the target job name. Once the task is scheduled in EasyTask, builds will be triggered automatically according to the schedule.

### Can I manage Jenkins jobs and views through EasyTask?

Yes. EasyTask provides full lifecycle management for Jenkins jobs and views. You can create jobs (with XML configuration), copy existing jobs, delete jobs, enable or disable jobs, and retrieve job information. For views, you can create views, update view configurations, delete views, and list all views. This allows you to centralize Jenkins administration within your EasyTask automated workflows.

## Next Steps

- [Integrations Overview](integrations_intro.md) — Learn about all available integrations in EasyTask.
- [GitHub Integration](github.md) — Connect your repositories and automate GitHub workflows.
- [Slack Integration](slack.md) — Send build notifications and alerts to your Slack channels.
