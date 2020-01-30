# Agent Settings

## Configuration Parameters

| Key | Description | Required | Type | Options | Default  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| agent\_key | Unique key that identifies Edge Delta agent for your company, given to you by the Edge Delta sales team. | No | String | N/A | N/A |
| ac\_buffer\_size | Defines the disk space the Edge Delta agent utilizes in memory in MB | No | Integer | 0 |  |
| tag | User defined prefix that agent writes on line that is processed | No | String | 1-128 characters or numbers | N/A |
| disable\_printer | Disable displaying agent process results on screen. Enabled by default. | No | Boolean | true/false | false |
| grace\_period | Time the agent waits before triggering alerts. Can be in seconds \(s\) or minutes \(m\) | No | String | 1-9999s | 0s |
| log \(group\) | If not specified, agent uses default log name as "edgedelta.log", default log level as "error and default log path as installation path | No |  |  |  |
| log/level | Logging level for the agent logs | No | Text | error, warning, info |  |
| log/path | Path of the agent log file | No | Text |  | N/A |
| resource\_limit \(group\) | Limit the resources agent consumes |  |  |  |  |
| resource\_limit/cpu\_utilization | Limit the max CPU consumption | No | Integer |  |  |
| resource\_limit/memory\_utilization\_limit\_inMB | Limit the max memory consumption in MB | No | Integer | 0 |  |
| resource\_limit/memory\_utilization\_limit\_percent | Limit the max memory consumption in percentage | No | Integer | 50 |  |
| resource\_limit/persistent\_storage\_size\_limit | Limit the max disk space agent can consume on the host | No | Integer | Unlimited |  |
| supervised\_learning \(group\) |  |  |  |  |  |
| supervised\_learning/enabled |  |  |  |  |  |
| supervised\_learning/sample\_msg\_count |  |  |  |  |  |
| supervised\_learning/once\_every |  |  |  |  |  |
| archive |  |  |  |  |  |
| misc |  |  |  |  |  |

Example:

```go
agent_settings:
  agent_key: 1234-A1B1-2345-1234
  ac_buffer_size: 128
  tag: QAServers
  disable_printer: true
  grace_period: 30s
  log:
    - level: error
    - path: e:\logs\myedgedelta.log
  resource_limit
    - cpu_utilization: 
    - memory_utilization_limit_inMB: 0
    - memory_utilization_limit_percent: 50
    - persistent_storage_size_limit: 1000
  supervised_learning
    - enabled: 
    - sample_msg_count
    - once_every
  archieve
  misc
```

