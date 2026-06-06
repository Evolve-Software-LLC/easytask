---
title: Email (SMTP) - EasyTask Integration Guide
description: Connect Email with EasyTask for automated workflow orchestration. Step-by-step setup, configuration, and best practices for sending emails programmatically via SMTP.
keywords:
  - email
  - smtp
  - easytask
  - workflow orchestration
  - automation
  - email notifications
---

# Email API

The Email API provides a simple operation for sending emails programmatically.

## Why Integrate Email with EasyTask?

Integrating Email (SMTP) with EasyTask enables you to automate email communications within your workflows. This integration allows you to:

- **Automate Email Notifications**: Send automated alerts, reports, and notifications as part of your EasyTask workflows without manual intervention.
- **Flexible Email Delivery**: Send HTML or plain text emails with custom subjects and bodies, supporting both TLS and non-TLS SMTP servers.
- **Integrate with Existing Infrastructure**: Connect to your organization's existing SMTP infrastructure seamlessly through EasyTask's vault-based credential management.

## Required Values in Vault

```
{
    "is_credentials": {
        "userid": "test",
        "passwd": "test123"
    },
    "integrations": {
        "secret": {
            "html_body": true,
            "password": "..XXXX..",
            "smtp_host": "XXX",
            "smtp_port": "XXXX...",
            "use_tls": false,
            "username": "XXXXXXX"
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
        "integration": "email",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "email/secret"
        },
        "action": [
            {
                "send_email": {
                    "to_address": "premswarup565@gmail.com",
                    "subject": "testing",
                    "body": "This is another test mail."
                }
            }
        ]
    }'
    ```

=== "Output"

    ```json
    
    {

        "integration": "genericsmtp",
        "uuid": "ae0e8ba9-423a-410e-bba5-e1933ff868c5",
        "init": {
            "vault_path_key": "email3/secret"
        },
        "error": false,
        "action": [
            {
                "send_email": true
            }
        ]
    }

    ```

## Functions

### `send_email`

**send_email**: This function sends an email to the specified recipient.

=== "Input Parameters"

    | Input Parameter | Type | Description | Mandatory |
    |----------------|------|-------------|-----------| 
    | to_address | str | Recipient's email address | yes |
    | subject | str | Subject of the email | yes |
    | body | str | Body content of the email | yes |

=== "Output"

    | Output Parameter | Type | Description |
    |-----------------|------|-------------|
    | response | bool | True if the email was sent successfully |

=== "JSON"

    ```json
    {
        "send_email": {
            "to_address": "premswarup565@gmail.com",
            "subject": "testing",
            "body": "This is another test mail."
        }
    }
    ```

---

## Frequently Asked Questions

### How do I configure Email credentials in EasyTask?
Use the EasyTask vault system to securely store your SMTP server credentials. Navigate to the integration configuration page and add your SMTP host, port, username, password, and TLS settings under a vault key like `email/secret`.

### Can I use Email with both EasyTask Cloud and On-Premises?
Yes, the Email SMTP integration works seamlessly with both EasyTask Cloud and On-Premises deployments. The configuration process is identical.

### How do I troubleshoot Email connection issues?
Check the integration server logs in EasyTask for detailed error messages. Verify your SMTP host, port, and credentials in the vault, ensure the SMTP server is accessible from the integration server, and test connectivity using the built-in connection test feature.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
