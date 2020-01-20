# Agent Settings

Schema:

```javascript
agent_settings:
  ac_buffer_size: 
  tag: 
  disable_printer: 
  grace_period: 
  log:
    - level: 
    - path:
```

| Setting | Required | Type | Options | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| agent\_key | Yes | GUID | GUID | N/A | Unique key that identifies Edge Delta agent for your company, given to you by the Edge Delta sales team. |
| ac\_buffer\_size | No | Integer | 0-9999 |  | Defines the space the Edge Delta agent utilizes in memory in MB |
| tag | No | Text | 1-128 characters or numbers | N/A | User defined prefix that agent writes on each line that is sent to an output. |
| disable\_printer | No | Boolean | true/false | false | Disables writing agent results on screen. By default it is enabled. |
| grace\_period | Yes | Time | 1-9999s | 0s | Grace period agent waits before triggering alerts. Can be in seconds \(s\), minutes \(m\) |
| log | No |  |  |  | If not specified, agent uses default name \(edgedelta.log\), default level \(error\) and default location \(path where agent ran\) |
| log/level | No | Text | error, warning, info |  | Logging level for the agent logs |
| log/path | No | Text |  | N/A | Path of the log file; if path is not specified, the log file is created  uses the path where the agent ran. |

Example:

```javascript
agent_settings:
  agent_key: 1234-A1B1-2345-1234
  ac_buffer_size: 125
  tag: QAServers
  disable_printer: true
  grace_period: 30s
  log:
    - level: error
    - path: e:\logs\myedgedelta.log
```

