# Agent Settings

## Configuration Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">agent_key</td>
      <td style="text-align:left">Unique key that identifies Edge Delta agent for your company, given to
        you by the Edge Delta sales team.</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">N/A</td>
    </tr>
    <tr>
      <td style="text-align:left">ac_buffer_size</td>
      <td style="text-align:left">Defines the disk space the Edge Delta agent utilizes in memory in MB</td>
      <td
      style="text-align:left">Integer</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">tag</td>
      <td style="text-align:left">User defined prefix that agent writes on line that is processed</td>
      <td
      style="text-align:left">String</td>
        <td style="text-align:left">N/A</td>
    </tr>
    <tr>
      <td style="text-align:left">disable_printer</td>
      <td style="text-align:left">Disable displaying agent process results on screen. Enabled by default.</td>
      <td
      style="text-align:left">Boolean</td>
        <td style="text-align:left">false</td>
    </tr>
    <tr>
      <td style="text-align:left">grace_period</td>
      <td style="text-align:left">Time the agent waits before triggering alerts. Can be in seconds (s) or
        minutes (m)</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">0s</td>
    </tr>
    <tr>
      <td style="text-align:left">log (group)</td>
      <td style="text-align:left">If not specified, agent uses default log name as &quot;edgedelta.log&quot;,
        default log level as &quot;error and default log path as installation path</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>log/</p>
        <p>level</p>
      </td>
      <td style="text-align:left">Logging level for the agent logs</td>
      <td style="text-align:left">Text</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>log/</p>
        <p>path</p>
      </td>
      <td style="text-align:left">Path of the agent log file</td>
      <td style="text-align:left">Text</td>
      <td style="text-align:left">N/A</td>
    </tr>
    <tr>
      <td style="text-align:left">resource_limit (group)</td>
      <td style="text-align:left">Limit the resources agent consumes</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>resource_limit/</p>
        <p>cpu_utilization</p>
      </td>
      <td style="text-align:left">Limit the max CPU consumption</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>resource_limit/</p>
        <p>memory_utilization_limit_inMB</p>
      </td>
      <td style="text-align:left">Limit the max memory consumption in MB</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>resource_limit/</p>
        <p>memory_utilization_limit_percent</p>
      </td>
      <td style="text-align:left">Limit the max memory consumption in percentage</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>resource_limit/</p>
        <p>persistent_storage_size_limit</p>
      </td>
      <td style="text-align:left">Limit the max disk space agent can consume on the host</td>
      <td style="text-align:left">Integer</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">supervised_learning (group)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>supervised_learning/</p>
        <p>enabled</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>supervised_learning/</p>
        <p>sample_msg_count</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>supervised_learning/</p>
        <p>once_every</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">archive</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">misc</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>Example:

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

