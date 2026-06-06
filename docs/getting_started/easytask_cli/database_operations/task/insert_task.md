---
title: Insert Task - EasyTask CLI - EasyTask Documentation
description: Insert a new task into the EasyTask database from a JSON or INI file using the database task insert CLI command.
keywords:
  - insert task
  - easytask cli
  - create task
  - task configuration
---

# Insert Task 

The `insert` command in the EasyTask CLI allows users to insert a new task into the database using information from a specified JSON or INI file. This command accepts a file path as an argument, which should point to a JSON or INI file containing the task details.

### Parameters

| Parameter | Description |
|-----------|-------------|
| `--file`  | Specifies the path to a JSON or INI file containing the task details to be inserted. This is a required parameter. |
| `--instance`  | Specifies the INSTANCE to which the task belongs. |

!!! Schema "Task Schema"

```json
  {                                                                                                                                                                                                                                                                                                                              
      "name": "new_twotask",                                                                                                                                    
      "task_owner": "data_team_change",                                                                                                                                   
      "cmd": "ls",                                                                                                                                                        
      "run_on_host": "payal",                                                                                                                                             
      "description": "updated Process daily data feed with alerts on success/failure",                                                                                            
      "stderr": "/tmp/data_process.err",                                                                                                                                  
      "stdout": "/tmp/data_process.out",                                                                                                                                  
      "timezone": "UTC",                                                                                                                                                  
      "active": true,                                                                                                                                                     
      "instance": "default",                                                                                                                                              
      "day_of_week": "1111100",                                                                                                                                           
      "trigger_times": "06:00",                                                                                                                                                                                                                                                                                   
      "run_as_user": "payal",                                                                                                                                         
      "max_run_time": 70,                                                                                                                                             
      "retry_attempts": 2,                                                                                                                                            
      "calendar": "US-Calendar",                                                                                                                                                                                                                                                                                                                                                                                                        
      "alert": {                                                                                                                                                          
          "integrations": [                                                                                                                                               
              {                                                                                                                                                           
                  "integration": "slack",                                                                                                                                 
                  "alert_on": "success",                                                                                                                                  
                  "init": {                                                                                                                                               
                      "vault_path_key": "slack/secret"                                                                                                                    
                  },                                                                                                                                                      
                  "action": [                                                                                                                                             
                      {                                                                                                                                                   
                          "send_message": {                                                                                                                               
                              "channel": "#data-ops",                                                                                                                     
                              "message": "Task ${T:task_id} ${T:task_name} completed successfully on ${E:YYYYMMDD}."                                                      
                          }                                                                                                                                               
                      }                                                                                                                                                   
                  ]                                                                                                                                                       
              },                                                                                                                                                          
              {                                                                                                                                                           
                  "integration": "slack",                                                                                                                                 
                  "alert_on": "failure",                                                                                                                                  
                  "init": {                                                                                                                                               
                      "vault_path_key": "slack/secret"                                                                                                                    
                  },                                                                                                                                                      
                  "action": [                                                                                                                                             
                      {                                                                                                                                                   
                          "send_message": {                                                                                                                               
                              "channel": "#data-alerts",                                                                                                                  
                              "message": "ALERT: Task ${T:task_name} (ID: ${T:task_id}) FAILED on ${E:YYYYMMDD}. Error: ${P:stderr}"                                      
                          }                                                                                                                                               
                      }                                                                                                                                                   
                  ]                                                                                                                                                       
              },                                                                                                                                                          
              {                                                                                                                                                           
                  "integration": "genericsmtp",                                                                                                                           
                  "alert_on": "failure",                                                                                                                                  
                  "init": {                                                                                                                                               
                      "vault_path_key": "email/smtp"                                                                                                                      
                  },                                                                                                                                                      
                  "action": [                                                                                                                                             
                      {                                                                                                                                                   
                          "send_email": {                                                                                                                                 
                              "to_address": "team@company.com",                                                                                                           
                              "subject": "TASK FAILED",                                                                                        
                              "body": "Task execution failed"                                                                            
                          }                                                                                                                                               
                      }                                                                                                                                                   
                  ]                                                                                                                                                       
              }                                                                                                                                                           
          ]                                                                                                                                                               
      }                                                                                                                                                                   
}         
```

## 🖥️ Basic Usage

```bash
easytask.bin database task insert -h 
usage: easytask.bin database task insert [-h] [--file FILE] [--instance INSTANCE]

options:
  -h, --help   show this help message and exit
  --file FILE  enter the path of the JSON/INI file containing the task.
  --instance INSTANCE  Instance name for independent tasks (not required if task belongs to a taskgroup)

```

### **Sample Input**
```
easytask.bin database task insert --file  /path/to/task.json --instance default

```

### **Sample Output**

```sh

Task Validations done. 
Task inserted successfully.
Insert Completed!

```


### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database task insert --file tasks/1.json --instance default

[INFO] Validating task: {'name': 'new_twotask', 'task_owner': 'data_team_change', 'cmd': 'ls', 'run_on_host': 'payal', 'description': 'Process daily data feed with alerts on success/failure', 'stderr': '/tmp/data_process.err', 'stdout': '/tmp/data_process.out', 'timezone': 'UTC', 'active': True, 'instance': 'default', 'day_of_week': '1111100', 'trigger_times': '06:00', 'run_as_user': 'payal', 'max_run_time': 70, 'retry_attempts': 2, 'calendar': 'US-Calendar', 'alert': {'integrations': [{'integration': 'slack', 'alert_on': 'success', 'init': {'vault_path_key': 'slack/secret'}, 'action': [{'send_message': {'channel': '#data-ops', 'message': 'Task ${T:task_id} ${T:task_name} completed successfully on ${E:YYYYMMDD}.'}}]}, {'integration': 'slack', 'alert_on': 'failure', 'init': {'vault_path_key': 'slack/secret'}, 'action': [{'send_message': {'channel': '#data-alerts', 'message': 'ALERT: Task ${T:task_name} (ID: ${T:task_id}) FAILED on ${E:YYYYMMDD}. Error: ${P:stderr}'}}]}, {'integration': 'genericsmtp', 'alert_on': 'failure', 'init': {'vault_path_key': 'email/smtp'}, 'action': [{'send_email': {'to_address': 'team@company.com', 'subject': 'TASK FAILED', 'body': 'Task execution failed'}}]}]}, 'tid': 2089} for INSERT

|[INFO]  Task inserted successfully.
|[INFO]  Insert Completed!
```

---

## Frequently Asked Questions

**Q: What file formats are supported for task insertion?**
A: Both JSON and INI file formats are supported for defining task configurations.

**Q: Do I need to specify `--instance` if the task belongs to a task group?**
A: The `--instance` parameter is not required if the task belongs to a task group, but is required for standalone tasks.

---

## Next Steps

- [Update Task](update_task.md) - Update an existing task
- [Query Task](query_task.md) - Look up task definitions
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI