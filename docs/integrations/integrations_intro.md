---
description: "EasyTask integration platform connects workflows to 30+ systems including PostgreSQL, Kafka, Jenkins, Slack, Jira, and more. Universal connectivity with enterprise security."
keywords: "EasyTask integrations, database connectors, Kafka, Jenkins, Slack, API integration, enterprise connectivity"
---

# EasyTask Integrations

## Enterprise Integration Platform

EasyTask provides a comprehensive integration ecosystem that connects your workflows to virtually any system in your technology stack. With 30+ pre-built integrations and a flexible plugin architecture, you can create seamless end-to-end automation that spans databases, cloud services, messaging systems, and business applications.

### Integration Architecture

Our integration platform is built on these core principles:

- **Universal Connectivity**: Connect to any system with REST APIs, databases, file systems, or message queues
- **Secure Communications**: All integrations support encryption, authentication, and secure credential management
- **Error Resilience**: Built-in retry logic, circuit breakers, and graceful error handling
- **Performance Optimized**: Connection pooling, caching, and efficient data transfer protocols
- **Monitoring Ready**: Complete observability into integration performance and health

---

## Integration Categories

### 🗄️ Database & Data Storage
Connect to relational databases, NoSQL systems, and data warehouses:

- **Relational**: PostgreSQL, MySQL, Oracle, SQL Server, SQLite
- **NoSQL**: MongoDB, CouchDB, CockroachDB, QuestDB
- **In-Memory**: Redis, Memcached, Hazelcast
- **Analytics**: TimescaleDB, H2, Apache Ignite
- **Cloud**: AWS RDS, Azure SQL, Google Cloud SQL

### ☁️ Cloud & Infrastructure
Integrate with major cloud platforms and infrastructure services:

- **AWS Services**: S3, Lambda, SQS, SNS, CloudWatch
- **Azure Services**: Blob Storage, Service Bus, Functions
- **Google Cloud**: Cloud Storage, Pub/Sub, Cloud Functions
- **Container**: Docker, Kubernetes, OpenShift
- **Monitoring**: Datadog, Splunk, Nagios, Elasticsearch

### 💬 Messaging & Communication
Connect to messaging systems and communication platforms:

- **Message Queues**: RabbitMQ, Apache Kafka, NSQ
- **Communication**: Slack, Microsoft Teams, Discord
- **Email & SMS**: SMTP, Twilio, SendGrid
- **Notifications**: Opsgenie, PagerDuty
- **Enterprise**: Skype for Business

### 💼 Business Applications
Integrate with enterprise and business applications:

- **Project Management**: Jira, ClickUp, ServiceNow
- **Documentation**: Confluence, SharePoint
- **Version Control**: Git, GitHub, GitLab, Bitbucket
- **CI/CD**: Jenkins, Azure DevOps, GitLab CI
- **Security**: OpenBao, CyberArk

### 🔌 APIs & Custom Integration
Flexible integration options for custom systems:

- **REST APIs**: HTTP/HTTPS with full authentication support
- **GraphQL**: Query and mutation support
- **SOAP**: Legacy system integration
- **FTP/SFTP**: File transfer protocols
- **SSH**: Remote command execution

## Supported Integrations

The Easytask Scheduler supports a wide range of integrations to enhance its functionality and adaptability. Below is a comprehensive list of supported tools and systems:

||| ✔️ [**ClickUp**](./clickup.md) | 🪳 [**CockroachDB**](./cockroach.md) | 📝 [**Confluence**](./confluence.md) | 🛋️ [**CouchDB**](./couchdb.md) ||
||------------------------------|---------------------------------------|-----------------------------------|-------------------------------------|
||| 🐕 [**Datadog**](./datadogs.md) | 🎮 [**Discord**](./discord.md) | 🔍 [**Elastic Search**](./elastic_search.md) | 📧 [**Email**](./email.md) ||
||| 📁 [**FTP**](./ftp.md) | 🐙 [**Github**](./github.md) | 📦 [**Git**](./git.md) | 🔄 [**H2**](./h2.md) ||
||| 🔷 [**Hazelcast**](./hazelcast.md) | 🌐 [**HTTP**](./http.md) | 🟡 [**HSQL**](./hsql.md) | 🟠 [**Apache Ignite**](./ignite.md) ||
||| 🐱 [**Jenkins**](./jenkins.md) | 🦋 [**Jira**](./jira.md) | 📡 [**Kafka**](./kafka.md) | 📦 [**Memcached**](./memcached.md) ||
||| 🍃 [**Mongodb**](./mongodb.md) | 🛢️ [**MSSQL**](./mssql.md) | 💬 [**MSTeams**](./msteams.md) | 🐬 [**MySQL**](./mysql.md) ||
||| 📊 [**NAGIOS**](./nagios.md) | 🗃️ [**NSQMQ**](./nsqmq.md) | 🔴 [**Oracle**](./oracle.md) | 🟢 [**Opsgenie**](./opsgenie.md) ||
||| 🐘 [**Postgresql**](./postgresql.md) | 🔵 [**QuestDB**](./questdb.md) | 🐰 [**RabbitMQ**](./rabbitmq.md) | ❤️ [**Redis**](./redis.md) ||
||| 🅱️ [**ServiceNow**](./servicenow.md) | 💙 [**Skype**](./skype.md) | 💜 [**Slack**](./slack.md) | 🌊 [**Solace**](./solance.md) ||
||| 🟣 [**Splunk**](./splunk.md) | 📄 [**SQLite**](./sqlite.md) | 🔐 [**SSH**](./ssh.md) | 📱 [**Twilio**](./twilio.md) ||
||| ⏱️ [**Timescale**](./timescale.md) | 🗝️ [**Vault**](./vault.md) | 🐘 [**Zookeeper**](./zookeeper.md) | ⭕ [**ZeroMQ**](./zeromq.md) ||

---

## Understanding the Integration Request Format

When you want EasyTask to perform an action using an integration, you send it a **request**. Think of this like filling out a form where you specify:
- Who you are (authentication)
- What integration you want to use
- What action you want to perform
- Any details needed for that action

### A Simple Example: Sending Metrics to Datadog

**What is Datadog?** It's a tool that monitors your computer systems and applications. You can send it information about how your systems are performing.

#### Step 1: Create an Integration Key and Set Up Credentials (One-Time Setup)

Before using any integration, you need to store your login information securely in the **OpenBao secret store** (a secure digital vault for passwords and keys).

!!! info "Two Ways to Create Integration Keys"
    You can create integration keys either through the **EasyTask Web Interface** (recommended, no technical knowledge required) or **directly via API** (for advanced users and automation).

---

##### Method 1: Using the EasyTask Web Interface (Recommended)

The web interface provides a user-friendly way to create and manage integration keys without any coding.

**Step 1: Access the Integration Manager**

1. Log in to the EasyTask Web Interface
2. Navigate to **Integrations** in the left sidebar
3. You'll see a table displaying all available integrations

**Step 2: Select Your Integration**

1. Find the integration you want to configure (e.g., "Datadog", "Slack", "PostgreSQL")
2. Click the **Manage** button (edit icon) next to the integration name
3. This opens the Key Management page for that integration

**Step 3: Create a New Integration Key**

On the Key Management page, you'll see a form with the following fields:

1. **Key Name** (Required)
   - Enter a unique name to identify this credential set
   - Example: `production-database`, `slack-notifications`, `datadog-monitoring`
   - Must be alphanumeric (letters and numbers only)
   - No spaces or special characters

2. **Path** (Auto-generated)
   - Automatically created as: `<integration_name>/<your_key_name>`
   - Example: `datadog/production`, `slack/notifications`
   - This path is used to reference the key in tasks

3. **Secret Configuration Form** (Dynamic fields)
   - The form automatically displays fields specific to your integration
   - Fields vary by integration type (see examples below)

**Integration-Specific Field Examples:**

??? example "Datadog Integration"
    When you select Datadog, the form will show:
    - **API Key**: Your Datadog API key
    - **Application Key**: Your Datadog application key
    - **Host URL**: Datadog server URL (e.g., `https://us5.datadoghq.com`)
    - **Proxy URL** (optional): Proxy server if required

??? example "Slack Integration"
    When you select Slack, the form will show:
    - **Bot Token**: Slack bot token (starts with `xoxb-`)
    - **User Token**: Slack user token (starts with `xoxp-`)

??? example "PostgreSQL Integration"
    When you select PostgreSQL, the form will show:
    - **Host**: Database server address
    - **Port**: Database port (default: 5432)
    - **Database**: Database name
    - **User**: Database username
    - **Password**: Database password

??? example "Email (SMTP) Integration"
    When you select Email, the form will show:
    - **SMTP Host**: Mail server address
    - **SMTP Port**: Mail server port
    - **Username**: Email username
    - **Password**: Email password
    - **Use TLS**: Toggle for TLS encryption (Yes/No)
    - **HTML Body**: Toggle for HTML emails (Yes/No)

**Step 4: Fill in the Required Information**

1. Enter a descriptive **Key Name**
2. Complete all required fields in the dynamic form
3. Optional fields may be left blank if not needed
4. The form validates your input in real-time

**Step 5: Save the Integration Key**

1. Click the **Save** button
2. EasyTask will:
   - Validate all fields
   - Encrypt and store the credentials in OpenBao
   - Save a reference in the database
3. On success, you'll see a confirmation message
4. The key will appear in the "Existing Keys" table below

**Step 6: Verify and Manage Your Keys**

After creating your keys, you can:
- **View** (eye icon): See the stored credentials in JSON format
- **Update** (edit icon): Modify existing credentials
- **Delete** (trash icon): Remove a key you no longer need

!!! tip "Best Practices for Key Names"
    - Use descriptive names that indicate purpose and environment
    - Examples: `prod-db`, `test-slack`, `dev-datadog`, `staging-s3`
    - This makes it easy to identify which key is used where
    - Consider including the environment (prod/dev/test) in the name

---

##### Method 2: Direct API Configuration (Advanced)

For advanced users who prefer API-based configuration or need to automate key creation:

**For Datadog, you need:**
1. Sign up at datadog.com
2. Get your API Key and Application Key
3. Store them in OpenBao with a path like "datadog/secret"

**What you store in OpenBao:**
```json
{
  "api_key": "your-actual-api-key-here",
  "app_key": "your-actual-app-key-here",
  "host_url": "https://us5.datadoghq.com"
}
```

**Why use the OpenBao secret store?**
- Your keys are encrypted and protected
- You don't have to type passwords every time
- If keys change, you only update them in one place
- Multiple team members can use integrations without sharing passwords
- Centralized audit logging of all credential access
- Role-based access control for sensitive credentials

#### Step 2: Send a Request to EasyTask

Here's a request that tells EasyTask to send performance data to Datadog:

```json
{
  "is_credentials": {
    "userid": "your-username",
    "passwd": "your-password"
  },
  "integrations": [
    {
      "integration": "datadog",
      "uuid": "unique-request-id-12345",
      "init": {
        "vault_path_key": "datadog/secret"
      },
      "action": [
        {
          "submit_metrics": {
            "metric_name": "website.response.time",
            "points": [
              {"timestamp": 1716704577, "value": 0.5},
              {"timestamp": 1716704567, "value": 0.3}
            ],
            "tags": ["environment:production", "server:web-1"]
          }
        }
      ]
    }
  ]
}
```

**Let's break down what each part means:**

| Section | What It Means | Simple Explanation |
|---------|---------------|-------------------|
| `is_credentials` | Your login information | Proves you're allowed to use EasyTask |
| `integration` | "datadog" | Which integration to use |
| `uuid` | "unique-request-id-12345" | A unique ID to track this specific request |
| `vault_path_key` | "datadog/secret" | Where to find your Datadog keys in OpenBao secret store |
| `action` | "submit_metrics" | What you want to do (send metrics) |
| `metric_name` | "website.response.time" | Name for the data you're sending |
| `points` | Array of values | The actual data (timestamps and values) |
| `tags` | Labels | Additional labels to organize your data |

#### Step 3: Receive the Response

After EasyTask completes your request, it sends back a response:

```json
{
  "integration": "datadog",
  "uuid": "unique-request-id-12345",
  "init": {
    "vault_path_key": "datadog/secret"
  },
  "error": false,
  "action": [
    {
      "submit_metrics": {
        "status": "success",
        "errors": []
      }
    }
  ]
}
```

**What the response tells you:**
- `error: false` - Everything worked correctly!
- `submit_metrics` - The action that was performed
- `status: "success"` - Confirms the metrics were sent
- `errors: []` - No errors occurred (empty list)

If something went wrong, `error` would be `true` and `errors` would contain details about what happened.

---

## Doing Multiple Things at Once

One of EasyTask's powerful features is that you can perform **multiple integration actions in a single request**. This is like having a multitasking assistant who can work on several things simultaneously.

### Example: Update Database AND Send Notification

Imagine you want to:
1. Save a new customer to your MySQL database
2. Send a Slack message to your sales team
3. Log the action in your monitoring system (Datadog)

**All in one request:**

```json
{
  "is_credentials": {
    "userid": "your-username",
    "passwd": "your-password"
  },
  "integrations": [
    {
      "integration": "mysql",
      "uuid": "request-1",
      "init": {
        "vault_path_key": "mysql/production"
      },
      "action": [
        {
          "insert_table": {
            "table": "customers",
            "records": [
              ["John Doe", "john@example.com", "555-1234"],
              ["Jane Smith", "jane@example.com", "555-5678"]
            ]
          }
        }
      ]
    },
    {
      "integration": "slack",
      "uuid": "request-2",
      "init": {
        "vault_path_key": "slack/sales-team"
      },
      "action": [
        {
          "send_message": {
            "channel": "#sales-updates",
            "message": "2 new customers added: John Doe and Jane Smith"
          }
        }
      ]
    },
    {
      "integration": "datadog",
      "uuid": "request-3",
      "init": {
        "vault_path_key": "datadog/monitoring"
      },
      "action": [
        {
          "submit_metrics": {
            "metric_name": "customers.added",
            "points": [{"timestamp": 1716704577, "value": 2}]
          }
        }
      ]
    }
  ]
}
```

**What happens:**
1. EasyTask connects to all three systems
2. Performs each action in order
3. If any action fails, it tells you which one and why
4. Returns results for all three actions

**Benefits:**
- **Faster**: All actions happen in one coordinated request
- **Reliable**: If one fails, you know exactly what succeeded and what didn't
- **Simpler**: One request instead of three separate ones
- **Traceable**: Each action has its own UUID for tracking

---

## Security: How Your Data Stays Safe

### 🔐 Multi-Layer Security

**1. Authentication (Proving Who You Are)**
- Every request requires encrypted credentials (userid and password)
- Credentials are verified before any action is taken
- Failed authentication attempts are logged

**2. Secure Credential Storage**
- Passwords, API keys, and secrets are stored in a secure secret store
- The secret store encrypts all secrets at rest
- Secrets are only decrypted when needed (in memory)
- You can rotate (change) secrets without updating code

### What This Means for You

✅ Your passwords are never stored in plain text
✅ Your data is encrypted during transmission
✅ Only authorized users can trigger actions
✅ Every action can be traced back to who requested it
✅ You can revoke access instantly if needed

---

## Common Use Cases

Here are some real-world examples of how organizations use EasyTask integrations:

### 🏥 Healthcare: Patient Data Management

**The Challenge**: Patient information needs to be securely stored, notifications sent to doctors, and reports generated automatically.

**The Solution**:
1. **PostgreSQL Integration**: Store patient records securely
2. **Slack Integration**: Notify on-call doctors of new admissions
3. **Email Integration**: Send automated appointment reminders
4. **Secret Store Integration**: Keep all patient data protected and compliant

**Result**: Reduced manual work by 80%, improved response times, ensured HIPAA compliance.

### 🛒 E-commerce: Order Processing

**The Challenge**: When a customer places an order, multiple systems need to be updated simultaneously.

**The Solution**:
1. **MySQL Integration**: Save order details to database
2. **Redis Integration**: Update inventory cache instantly
3. **Slack Integration**: Alert fulfillment team
4. **Twilio Integration**: Send SMS confirmation to customer
5. **Datadog Integration**: Track order volume metrics

**Result**: Orders processed in under 2 seconds, zero data loss, real-time inventory updates.

### 💼 Software Development: CI/CD Pipeline

**The Challenge**: When developers update code, it needs to be tested, deployed, and stakeholders notified.

**The Solution**:
1. **GitHub Integration**: Detect new code commits
2. **Jenkins Integration**: Run automated tests
3. **Slack Integration**: Notify team of test results
4. **Jira Integration**: Update task status automatically
5. **Email Integration**: Send release notes to stakeholders

**Result**: Deployment time reduced from hours to minutes, fewer errors, better communication.

### 📊 Business Intelligence: Report Generation

**The Challenge**: Management needs daily reports combining data from multiple systems.

**The Solution**:
1. **Multiple Database Integrations**: Pull data from various sources
2. **MongoDB Integration**: Store combined results
3. **Email Integration**: Send formatted reports every morning
4. **Slack Integration**: Alert team if reports are ready or if issues occur

**Result**: Saved 10+ hours per week in manual report preparation, improved data accuracy.

---

## Frequently Asked Questions

### What systems can EasyTask integrate with?
EasyTask integrates with 30+ external systems across five major categories: databases (PostgreSQL, MySQL, Oracle, MongoDB, Redis), cloud services (AWS, Azure, Google Cloud), messaging platforms (Kafka, RabbitMQ, Slack, Microsoft Teams), CI/CD tools (Jenkins, GitHub, GitLab), and business applications (Jira, ServiceNow, ClickUp). It also supports custom integrations via REST APIs, GraphQL, FTP/SFTP, and SSH.

### How do EasyTask integrations handle errors and retries?
Every EasyTask integration includes built-in error resilience through automatic retry logic, circuit breakers, and graceful error handling. When an integration action fails, EasyTask reports exactly which action failed and why, while preserving the results of successful actions. Integration credentials are securely stored in the OpenBao secret store with encrypted storage, and secrets can be rotated without updating task configurations.

### Can I build custom integrations for EasyTask?
Yes. EasyTask provides a flexible plugin architecture and multiple integration options for custom systems. You can connect to any system using REST APIs with full authentication support, GraphQL queries, SOAP for legacy systems, FTP/SFTP for file transfers, or SSH for remote command execution. The platform also offers comprehensive APIs, CLI tools, and SDK support for building tailored integration solutions.

## Next Steps

- [Set up another integration](index.md)
- [Configure task schedules](../getting_started/tasks/task.md)
- [Explore worker agents](../getting_started/components/worker_agent.md)
