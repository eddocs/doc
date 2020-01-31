# Agent Settings

## Configuration Parameters

| Key | Description | Default  |
| :--- | :--- | :--- |
| agent\_key | Unique key that identifies Edge Delta agent for your company, given to you by the Edge Delta sales team. | N/A |
| ac\_buffer\_size | Defines the disk space the Edge Delta agent utilizes in memory in MB |  |
| tag | User defined prefix that agent writes on line that is processed | N/A |
| disable\_printer | Disable displaying agent process results on screen. Enabled by default. | false |
| grace\_period | Time the agent waits before triggering alerts. Can be in seconds \(s\) or minutes \(m\) | 0s |
| _log_  | If omitted, agent uses default log name as "edgedelta.log", default log level as "error and default log path as installation path |  |
| level | Logging level for the agent logs |  |
| path | Path of the agent log file | N/A |
| _supervised\_learning_  |  |  |
| enabled | Enable or disable the supervised learning feature |  |
| sample\_msg\_count |  |  |
| once\_every |  |  |

Example:

```go
agent_settings:
  agent_key: 1234-A1B1-2345-1234
  ac_buffer_size: 128
  tag: QAServers
  disable_printer: true
  grace_period: 30s
  log:
    level: error
    path: e:\logs\myedgedelta.log
  supervised_learning:
    enabled: true
    sample_msg_count: 100
    once_every: 1h
```

