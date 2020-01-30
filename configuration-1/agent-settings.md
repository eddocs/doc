# Agent Settings

## Configuration Parameters

| Key | Description | Default  |
| :--- | :--- | :--- |
| agent\_key | Unique key that identifies Edge Delta agent for your company, given to you by the Edge Delta sales team. | N/A |
| ac\_buffer\_size | Defines the disk space the Edge Delta agent utilizes in memory in MB |  |
| tag | User defined prefix that agent writes on line that is processed | N/A |
| disable\_printer | Disable displaying agent process results on screen. Enabled by default. | false |
| grace\_period | Time the agent waits before triggering alerts. Can be in seconds \(s\) or minutes \(m\) | 0s |
| log \(group\) | If not specified, agent uses default log name as "edgedelta.log", default log level as "error and default log path as installation path |  |
|  - level | Logging level for the agent logs |  |
|  - path | Path of the agent log file | N/A |
| resource\_limit \(group\) | Limit the resources agent consumes |  |
|  - cpu\_utilization | Limit the max CPU consumption |  |
|  - memory\_utilization\_limit\_inMB | Limit the max memory consumption in MB |  |
|  - memory\_utilization\_limit\_percent           | Limit the max memory consumption in percentage |  |
|  - persistent\_storage\_size\_limit | Limit the max disk space agent can consume on the host |  |
| supervised\_learning \(group\) |  |  |
|  - enabled |  |  |
|  - sample\_msg\_count |  |  |
|  - once\_every |  |  |
| archive |  |  |
| misc |  |  |

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
  resource_limit:
    - cpu_utilization: 
    - memory_utilization_limit_inMB: 0
    - memory_utilization_limit_percent: 50
    - persistent_storage_size_limit: 1000
  supervised_learning:
    - enabled: 
    - sample_msg_count
    - once_every
  archieve
  misc
```

