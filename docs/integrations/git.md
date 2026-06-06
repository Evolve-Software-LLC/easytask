---
title: Git - EasyTask Integration Guide
description: Connect Git with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing Git repositories, branches, and version control.
keywords:
  - git
  - easytask
  - workflow orchestration
  - automation
  - version control
  - repository management
---

# Git API

The Git API provides a set of endpoints for managing Git repositories, branches, and performing various Git operations. It allows users to interact with Git repositories programmatically.

## Why Integrate Git with EasyTask?

Integrating Git with EasyTask enables you to automate version control and repository management workflows. This integration allows you to:

- **Automate Repository Operations**: Clone, initialize, and manage Git repositories automatically as part of your EasyTask workflows without manual intervention.
- **Streamline Branch and Tag Management**: Create branches, switch contexts, create and delete tags, and manage your release workflow programmatically through EasyTask orchestration.
- **Automate Commit and Sync Workflows**: Stage changes, commit, push, pull, and fetch from remotes automatically, enabling continuous integration and deployment pipelines.

## Required Values in Vault

```
{
   "secret": {
         "github_auth_token": "xxxxxxxx (String Type)"
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
        "integration": "git",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "git/secret"
        },
        "action": [
            {
                "clone": {
                    "repo_link": "http://192.158.238.91:3000/clouduser3/test.empty.git",
                    "no_checkout": false,
                    "reject_shallow": false,
                    "bare": false
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {
        "integration": "git",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "git/server1",
            "working_dir": ""
        },
        "error": false,
        "action": [
            {
                "clone": ""
            }
        ]
    }

    ```

## Functions

### `clone`

**clone**: This function clones a Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_link | str | URL of the repository to clone | yes |
    | no_checkout | bool | If true, don't checkout HEAD after cloning | no |
    | reject_shallow | bool | If true, reject shallow clones | no |
    | bare | bool | If true, create a bare repository | no |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of successful cloning |

=== "JSON"

    ```json
    {
        "clone": {
            "repo_link": "http://192.158.238.91:3000/clouduser3/test.empty.git",
            "no_checkout": false,
            "reject_shallow": false,
            "bare": false
        }
    }
    ```

### `return_working_dir`

**return_working_dir**: This function returns the current working directory.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Current working directory path |

=== "JSON"

    ```json
    {
        "return_working_dir": {}
    }
    ```

### `change_working_dir`

**change_working_dir**: This function changes the current working directory.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | path | str | Path to the new working directory | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of directory change |

=== "JSON"

    ```json
    {
        "change_working_dir": {
            "path": "testempty"
        }
    }
    ```

### `init`

**init**: This function initializes a new Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | directory | str | Directory to initialize the repository in | no |
    | bare | bool | If true, create a bare repository | no |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of repository initialization |

=== "JSON"

    ```json
    {
        "init": {
            "directory": "",
            "bare": false
        }
    }
    ```

### `get_repo_status`

**get_repo_status**: This function retrieves the status of the Git repository.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Repository status information |

=== "JSON"

    ```json
    {
        "get_repo_status": {}
    }
    ```

### `create_branch`

**create_branch**: This function creates a new branch in the Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | branch_name | str | Name of the new branch | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of branch creation |

=== "JSON"

    ```json
    {
        "create_branch": {
            "branch_name": "test-branch"
        }
    }
    ```

### `list_branches`

**list_branches**: This function lists all branches in the Git repository.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of branch names |

=== "JSON"

    ```json
    {
        "list_branches": {}
    }
    ```

### `select_branch`

**select_branch**: This function checks out a specified branch.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | branch_name | str | Name of the branch to checkout | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of branch checkout |

=== "JSON"

    ```json
    {
        "select_branch": {
            "branch_name": "test-branch"
        }
    }
    ```

### `create_tag`

**create_tag**: This function creates a new tag in the Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | tag_name | str | Name of the new tag | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of tag creation |

=== "JSON"

    ```json
    {
        "create_tag": {
            "tag_name": "V1"
        }
    }
    ```

### `delete_tag`

**delete_tag**: This function deletes a tag from the Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | tag_name | str | Name of the tag to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of tag deletion |

=== "JSON"

    ```json
    {
        "delete_tag": {
            "tag_name": "V1"
        }
    }
    ```

### `stage_changes`

**stage_changes**: This function stages all changes in the Git repository.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of staging changes |

=== "JSON"

    ```json
    {
        "stage_changes": {}
    }
    ```

### `commit`

**commit**: This function commits staged changes to the Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | message | str | Commit message | yes |
    | allow_empty | bool | If true, allow empty commits | no |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of commit |

=== "JSON"

    ```json
    {
        "commit": {
            "message": "this is a test commit",
            "allow_empty": true
        }
    }
    ```

### `get_modified_files`

**get_modified_files**: This function retrieves a list of modified files in the Git repository.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of modified file names |

=== "JSON"

    ```json
    {
        "get_modified_files": {}
    }
    ```

### `get_file_version`

**get_file_version**: This function retrieves the version of a specific file in the Git repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | file_name | str | Name of the file to check | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Version information of the file |

=== "JSON"

    ```json
    {
        "get_file_version": {
            "file_name": "a.txt"
        }
    }
    ```

### `get_commit_count`

**get_commit_count**: This function retrieves the total number of commits in the Git repository.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Total number of commits |

=== "JSON"

    ```json
    {
        "get_commit_count": {}
    }
    ```

### `fetch_all`

**fetch_all**: This function fetches updates from all remotes.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of fetch operation |

=== "JSON"

    ```json
    {
        "fetch_all": {}
    }
    ```

### `pull`

**pull**: This function pulls changes from a remote repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the remote repository | yes |
    | branch_name | str | Name of the branch to pull from | yes |
    | rebase | bool | If true, rebase instead of merge | no |
    | no_commit | bool | If true, don't commit after pull | no |
    | verbose | bool | If true, be more verbose | no |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of pull operation |

=== "JSON"

    ```json
    {
        "pull": {
            "repo_name": "origin",
            "branch_name": "master",
            "rebase": false,
            "no_commit": false,
            "verbose": false
        }
    }
    ```

### `get_commit_keys`

**get_commit_keys**: This function retrieves commit keys for a specific branch.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | branch_name | str | Name of the branch | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of commit keys |

=== "JSON"

    ```json
    {
        "get_commit_keys": {
            "branch_name": "test-branch"
        }
    }
    ```

### `get_log`

**get_log**: This function retrieves the log for a specific commit.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | commit_ID | str | ID of the commit | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Commit log information |

=== "JSON"

    ```json
    {
        "get_log": {
            "commit_ID": "c6254ab28bc296ef52ab74586bf32b145d733643"
        }
    }
    ```

### `get_diffs`

**get_diffs**: This function retrieves the differences between two commits.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | commit_ID1 | str | ID of the first commit | yes |
    | commit_ID2 | str | ID of the second commit | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Differences between the two commits |

=== "JSON"

    ```json
    {
        "get_diffs": {
            "commit_ID1": "c6254ab28bc296ef52ab74586bf32b145d733643",
            "commit_ID2": "72515fdff383f6a3ba27eff3b15dd34b412a360d"
        }
    }
    ```

### `push`

**push**: This function pushes changes to a remote repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | host_domain | str | Domain of the remote host | yes |
    | remote_username | str | Username for the remote repository | yes |
    | remote_repo_name | str | Name of the remote repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of push operation |

=== "JSON"

    ```json
    {
        "push": {
            "host_domain": "192.158.238.91:3000",
            "remote_username": "clouduser3",
            "remote_repo_name": "testempty"
        }
    }
    ```

### `delete_branch_remote`

**delete_branch_remote**: This function deletes a branch from a remote repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | host_domain | str | Domain of the remote host | yes |
    | remote_username | str | Username for the remote repository | yes |
    | remote_repo_name | str | Name of the remote repository | yes |
    | branch_name | str | Name of the branch to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Confirmation message of branch deletion |

=== "JSON"

    ```json
    {
        "delete_branch_remote": {
            "host_domain": "192.158.238.91:3000",
            "remote_username": "clouduser3",
            "remote_repo_name": "testempty",
            "branch_name": "test-branch"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Git credentials in EasyTask?
Use the EasyTask vault system to securely store your Git authentication token. Navigate to the integration configuration page and add your GitHub auth token under a vault key like `git/secret`.

### Can I use Git with both EasyTask Cloud and On-Premises?
Yes, Git works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot Git connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your auth token in the vault, ensure the Git server is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
