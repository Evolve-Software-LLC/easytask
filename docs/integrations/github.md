---
title: GitHub - EasyTask Integration Guide
description: Connect GitHub with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for managing repositories, issues, and pull requests.
keywords:
  - github
  - easytask
  - workflow orchestration
  - automation
  - repository management
  - continuous integration
---

# GitHub API

The GitHub API provides a set of endpoints for interacting with GitHub repositories, issues, pull requests, and more. It allows users to programmatically manage their GitHub accounts and projects.

## Why Integrate GitHub with EasyTask?

Integrating GitHub with EasyTask enables you to automate repository management and development workflows. This integration allows you to:

- **Automate Repository Lifecycle**: Create, clone, and delete repositories programmatically as part of your EasyTask workflows without manual intervention.
- **Streamline Issue Management**: Create and close GitHub issues automatically, keeping your project tracking in sync with your automated workflows.
- **Manage Code and Files**: Create, update, upload, and delete files in your repositories through EasyTask orchestration, enabling automated deployment and content management pipelines.

## Required Values in Vault

```
{
    "is_credentials": {
        "userid": "test",
        "passwd": "test123"
    },
    "integrations": {
        "integration": "github",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "github/server1"
        }
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
        "integration": "github",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "github/secret"
        },
        "action": [
            {
                "see_user": {}
            }
        ]
    }'
    ```

=== "Output"

    ```json
    {
        "see_user": {
            "login": "your_username",
            "id": 12345678,
            "name": "Your Name",
            "email": "your_email@example.com"
        }
    }
    ```

## Functions

### `see_user`

**see_user**: This function retrieves information about the authenticated user.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | User information including login, id, name, and email |

=== "JSON"

    ```json
    {
        "see_user": {}
    }
    ```

### `see_repos`

**see_repos**: This function lists all repositories for the authenticated user.

=== "Input Parameters"

    This function takes no input parameters.

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of repository information |

=== "JSON"

    ```json
    {
        "see_repos": {}
    }
    ```

### `clone_repo`

**clone_repo**: This function clones one or more repositories.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repos | list | List of repository names to clone | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of cloning operation for each repository |

=== "JSON"

    ```json
    {
        "clone_repo": {
            "repos": ["test2"]
        }
    }
    ```

### `create_repo`

**create_repo**: This function creates a new repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | full_name | str | Name of the new repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the newly created repository |

=== "JSON"

    ```json
    {
        "create_repo": {
            "full_name": "newrepo"
        }
    }
    ```

### `delete_repo`

**delete_repo**: This function deletes one or more repositories.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repos | list | List of repository names to delete | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of deletion operation for each repository |

=== "JSON"

    ```json
    {
        "delete_repo": {
            "repos": ["newrepo"]
        }
    }
    ```

### `count_of_stars`

**count_of_stars**: This function retrieves the number of stars for a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | int | Number of stars for the repository |

=== "JSON"

    ```json
    {
        "count_of_stars": {
            "repo_name": "test2"
        }
    }
    ```

### `get_labels`

**get_labels**: This function retrieves the labels for a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of labels for the repository |

=== "JSON"

    ```json
    {
        "get_labels": {
            "repo_name": "test2"
        }
    }
    ```

### `create_file`

**create_file**: This function creates a new file in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | file_name | str | Name of the file to create | yes |
    | content | str | Content of the file | yes |
    | message | str | Commit message | yes |
    | branch | str | Branch to create the file in | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the created file |

=== "JSON"

    ```json
    {
        "create_file": {
            "repo_name": "test2",
            "file_name": "hi.txt",
            "content": "Hello World",
            "message": "Commit new File",
            "branch": "main"
        }
    }
    ```

### `upload_files`

**upload_files**: This function uploads multiple files to a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | file_names | list | List of file names to upload | yes |
    | message | str | Commit message | yes |
    | branch | str | Branch to upload the files to | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of upload operation for each file |

=== "JSON"

    ```json
    {
        "upload_files": {
            "repo_name": "test2",
            "file_names": ["hi.txt"],
            "message": "Commit new File",
            "branch": "main"
        }
    }
    ```

### `update_file`

**update_file**: This function updates an existing file in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | file_name | str | Name of the file to update | yes |
    | new_content | str | New content of the file | yes |
    | message | str | Commit message | yes |
    | branch | str | Branch containing the file | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the updated file |

=== "JSON"

    ```json
    {
        "update_file": {
            "repo_name": "test2",
            "file_name": "hi.txt",
            "new_content": "Hello World updated",
            "message": "Commit new File",
            "branch": "main"
        }
    }
    ```

### `update_local_files`

**update_local_files**: This function updates local files and pushes changes to a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | file_names | list | List of file names to update | yes |
    | message | str | Commit message | yes |
    | branch | str | Branch to update | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of update operation for each file |

=== "JSON"

    ```json
    {
        "update_local_files": {
            "repo_name": "test2",
            "file_names": ["hi.txt"],
            "message": "Commit new File",
            "branch": "main"
        }
    }
    ```

### `delete_files`

**delete_files**: This function deletes files from a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | file_names | list | List of file names to delete | yes |
    | message | str | Commit message | yes |
    | branch | str | Branch containing the files | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of deletion operation for each file |

=== "JSON"

    ```json
    {
        "delete_files": {
            "repo_name": "test2",
            "file_names": ["hi.txt"],
            "message": "Commit new File",
            "branch": "main"
        }
    }
    ```

### `createissue`

**createissue**: This function creates a new issue in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo | str | Name of the repository | yes |
    | issue | str | Description of the issue | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the created issue |

=== "JSON"

    ```json
    {
        "createissue": {
            "repo": "test2",
            "issue": "This is the issue i have created"
        }
    }
    ```

### `closeissue`

**closeissue**: This function closes an issue in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo | str | Name of the repository | yes |
    | issue_milestone | int | Milestone number of the issue to close | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of the issue closure operation |

=== "JSON"

    ```json
    {
        "closeissue": {
            "repo": "test2",
            "issue_milestone": 10
        }
    }
    ```

### `open_issues`

**open_issues**: This function retrieves open issues for a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of open issues for the repository |

=== "JSON"

    ```json
    {
        "open_issues": {
            "repo_name": "test2"
        }
    }
    ```

### `list_branches`

**list_branches**: This function lists all branches in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of branches in the repository |

=== "JSON"

    ```json
    {
        "list_branches": {
            "repo_name": "test2"
        }
    }
    ```

### `create_branch`

**create_branch**: This function creates a new branch in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | source_branch | str | Name of the source branch | yes |
    | target_branch | str | Name of the new branch to create | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the created branch |

=== "JSON"

    ```json
    {
        "create_branch": {
            "repo_name": "test2",
            "source_branch": "main",
            "target_branch": "newbranch"
        }
    }
    ```

### `checkout_branch`

**checkout_branch**: This function checks out a branch in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | branch | str | Name of the branch to checkout | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | str | Status of the checkout operation |

=== "JSON"

    ```json
    {
        "checkout_branch": {
            "repo_name": "test2",
            "branch": "newbranch"
        }
    }
    ```

### `create_pullrequest`

**create_pullrequest**: This function creates a new pull request in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | source_branch | str | Name of the source branch | yes |
    | target_branch | str | Name of the target branch | yes |
    | title | str | Title of the pull request | yes |
    | body | str | Description of the pull request | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Information about the created pull request |

=== "JSON"

    ```json
    {
        "create_pullrequest": {
            "repo_name": "test2",
            "source_branch": "main",
            "target_branch": "newbranch",
            "title": "title of pull request",
            "body": "Body of pull request"
        }
    }
    ```

### `list_pullrequests`

**list_pullrequests**: This function lists all pull requests in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of pull requests in the repository |

=== "JSON"

    ```json
    {
        "list_pullrequests": {
            "repo_name": "test2"
        }
    }
    ```

### `merge_pullrequest`

**merge_pullrequest**: This function merges a pull request in a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | repo_name | str | Name of the repository | yes |
    | pull_request | int | Number of the pull request to merge | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | dict | Status of the merge operation |

=== "JSON"

    ```json
    {
        "merge_pullrequest": {
            "repo_name": "test2",
            "pull_request": 10
        }
    }
    ```

### `acces_logs`

**acces_logs**: This function retrieves access logs for a repository.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | path | str | Path to the repository | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | list | List of access log entries |

=== "JSON"

    ```json
    {
        "acces_logs": {
            "path": "test2"
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure GitHub credentials in EasyTask?
Use the EasyTask vault system to securely store your GitHub connection credentials. Navigate to the integration configuration page and add your server details under a vault key like `github/server1`.

### Can I use GitHub with both EasyTask Cloud and On-Premises?
Yes, GitHub works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical since GitHub is a cloud-based service.

### How do I troubleshoot GitHub connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your credentials in the vault, ensure the GitHub API is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
