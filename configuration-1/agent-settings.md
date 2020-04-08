---
description: >-
  This document outlines the agent level parameters that can be defined as part
  of the Edge Delta agent's configuration file.
---

# Agent Settings

## Configuration Parameters

| Key | Description | Default  | Required |
| :--- | :--- | :--- | :--- |
| ac\_buffer\_size | Anomaly Capture buffer size, represents the number of log lines to capture during an anomaly capture | 125 | No |
| tag | User defined tag to describe the server type, environment, etc. for the host the agent will be deployed on. Metrics output by the agent to backend systems will have this tag included. Example: prod\_payments | Edge | No |
| disable\_printer | Disable displaying agent process results on screen. Enabled by default | false | No |
| grace\_period | Time the agent waits before triggering alerts. Can be in seconds \(s\) or minutes \(m\) | 0s | No |
| _**log**_ **** | If omitted, agent uses default log name "edgedelta.log", default log level as "info" and default log path as installation path | N/A | No |
| level | Logging level for the agent logs | info | No |
| path | Custom path to output the agent's log file to | edgedelta.log | No |
| _**supervised\_learning**_  | Supervised learning enables the Edge Delta agent to periodically sample incoming data to help generate rules and monitors | N/A | No |
| enabled | Enable or disable the supervised learning feature | false | No |
| sample\_msg\_count | How many messages the agent should sample when supervised learning is enabled | 100 | No |
| once\_every | How frequently the agent should sample incoming data when supervised learning is enabled | 1h | No |
| _**archive**_ | Archive allows the Edge Delta agent to forward raw datasets to 3rd party systems for archival purposes, such as S3 | N/A | No |
| name | User-defined name of this particular Archive destination | s3 | Yes \(if archive enabled\) |
| aws\_key\_id | AWS Key ID for IAM user w/bucket access | N/A | Yes \(if archive enabled\) |
| aws\_sec\_key | AWS Security Key for IAM user w/bucket access | N/A | Yes \(if archive enabled\) |
| s3\_bucket | Name of S3 bucket | N/A | Yes \(if archive enabled\) |
| s3\_region | Region of S3 bucket | N/A | Yes \(if archive enabled\) |
| size | Buffer size before sending data to archive destination | 16mb | Yes \(if archive enabled\) |
| compress | Compression type for archived data | gzip | Yes \(if archive enabled\) |
| **buffer** | \(Archive Buffer\) Rather than in-memory buffering, provide disk location to store temporary buffer | Buffered in-memory | No |
| path | User defined path to temporarily store buffered data before archiving | N/A | Yes \(if buffer enabled\) |

Example:

```go
agent_settings:
  ac_buffer_size: 125
  tag: prod_payments
  disable_printer: true
  grace_period: 30s
  log:
    level: error
    path: /var/log/edgedelta.log
  supervised_learning:
    enabled: true
    sample_msg_count: 100
    once_every: 1h
```

