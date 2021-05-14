---
description: >-
  This document outlines the agent level parameters that can be defined as part
  of the Edge Delta agent's configuration file.
---

# Agent Settings

## Configuration Parameters

| Key | Description | Default  | Required |
| :--- | :--- | :--- | :--- |
| tag | User defined tag to describe the server type, environment, etc. for the host the agent will be deployed on. Metrics output by the agent to backend systems will have this tag included. Example: prod\_payments | Edge | No |
| anomaly\_capture\_size | Anomaly Capture buffer size represents the number of log lines to capture during an anomaly capture | 125 | No |
| anomaly\_capture\_bytesize | Anomaly Capture buffer byte size represents the maximum buffer size in terms of bytes during an anomaly capture | 0 B (disabled) | No |
| anomaly\_capture\_duration | Anomaly Capture buffer duration represents the maximum span that the logs of an anomaly capture can belong to | 0s (disabled) | No |
| capture\_flush\_mode | Sets the behavior of flushing captured contextual log buffers. Supported modes are listed below: <br> **local_per_source**: This is the default mode. captured buffer of a source is flushed when there's a local alert being triggered from same source. <br> **local_all**: This is the mode where all captured buffers are flushed when there's a local alert being triggered (not necessarily from same source). So in this mode whenever an alert is triggered from agent all capture buffers from all active sources will be flushed <br> **tag_per_source**: This is the mode where captured buffer of a source is flushed when there's an alert from same source and tag (from any agent within current tag) <br> **tag_all**: This is the mode where all captured buffers on all agents within the same tag is flushed whenever any of the agents trigger an alert| local_per_source | No |
| grace\_period | Time the agent waits before triggering alerts. Can be in seconds \(s\) or minutes \(m\) | 0s | No |
| misc | Other miscellaneous mappings that you want to append to config | - | No |
| ephemeral | It is only honored by clustering processor at the moment. 0.5 means 50% of a core. It can be enabled by setting cpu_friendly=true in clustering rule. | true | No |
| soft\_cpu\_limit | It marks the agent as can be down temporarily due to scale down scenarios and it will be used for capturing down agents | 0.0 | No |
| anomaly\_tolerance | When it is non-zero, anomaly scores handle edge cases better when standard deviation is too small. Can be set at rule level for some rule types. | 0.01 | No |
| anomaly\_confidence\_period | Anomaly scores will not be calculated for the first this period after a source is found. Can be set at rule level for some rule types. | 30m | No |
| anomaly\_coefficient | Anomaly coefficient is used to multiple final score to [0, 100] range. The higher the coefficient the higher the anomaly score will be. Can be set at rule level for some rule types. | 10 | No |
| skip\_empty\_intervals | Skips empty intervals when rolling so the anomaly scores are calculated based on history of non-zero intervals. Can be set at rule level for some rule types. | false | No |
| only\_report\_nonzeros | Only report non zero stats. Can be set at rule level for some rule types. | false | No |
| _**log**_ | If omitted, agent uses default log name "edgedelta.log", default log level as "info" and default log path as installation path | N/A | No |
| level | Logging level for the agent logs | info | No |
| _**archive**_ | Archive allows the Edge Delta agent to forward raw datasets to 3rd party systems for archival purposes, such as S3 | N/A | No |
| name | User-defined name of this particular Archive destination | s3 | Yes \(if archive enabled\) |
| aws\_key\_id | AWS Key ID for IAM user w/bucket access | N/A | No \(if archive enabled, and credential\_path set\) |
| aws\_sec\_key | AWS Security Key for IAM user w/bucket access | N/A | No \(if archive enabled, and credential\_path set\) |
| credential\_path | Path to where the credentials are stored, can be used instead of aws\_key\_id and aws\_sec\_key | N/A | No \(if archive enabled, and aws\_key\_id and ws\_sec\_key set\) |
| s3\_bucket | Name of S3 bucket | N/A | Yes \(if archive enabled\) |
| s3\_region | Region of S3 bucket | N/A | Yes \(if archive enabled\) |
| compress | Compression type for archived data | gzip | Yes \(if archive enabled\) |
| size | Buffer size before sending data to archive destination | 16mb | Yes \(if archive enabled\) |
| **buffer** | \(Archive Buffer\) Rather than in-memory buffering, provide disk location to store temporary buffer | Buffered in-memory | No |
| path | User defined path to temporarily store buffered data before archiving | N/A | Yes \(if buffer enabled\) |


Example:

```go
agent_settings:
  tag: prod_payments
  log:
    level: error
  soft_cpu_limit: 0.5
  anomaly_tolerance: 0.1
  anomaly_confidence_period: 1m
  skip_empty_intervals: false
  only_report_nonzeros: false
  anomaly_capture_size: 1000
  anomaly_capture_bytesize: "10 KB"
  anomaly_capture_duration: 1m
  anomaly_coefficient: 10.0
  grace_period: 30s
  archive:
    name: "s3"
    aws_key_id: "<key_id_for_iam_user>"
    aws_sec_key: "<sec_key_for_iam_user"
    s3_bucket: "<name_of_s3_bucket>"
    s3_region: "<region_of_s3_bucket>"
    size: "1MB"
    buffer:
      # setting buffer's path will enable file buffering to reduce agent's memory usage. Make sure agent has write access to provided path.
      path: "/var/log/edgedelta/archive"
```
