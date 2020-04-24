---
description: >-
  This document outlines the various Processor types supported by the Edge Delta
  service, and how the processors are configured.
---

# Processors

## Overview

Processors are the mechanism used to allow users to specify various analytical, statistical, and machine-learning based algorithms to apply to their incoming data. 

The labels are used to map processors to specific inputs and outputs, as part of a workflow. 

## Cluster

If enabled, the cluster processor will apply realtime clustering algorithms to the specified inputs as part of a workflow. The clustering algorithms automatically detect the structure, and patterns of each incoming event, providing a comprehensive analysis of all incoming data. In addition, clustering provides a unique analysis of incoming data streams to make detecting log-based anomalies extremely simple. 

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific processor, used for mapping this processor to a workflow | Yes |
| num\_of\_clusters | Max number of clusters to generate for a given input.  | Yes |
| samples\_per\_cluster | The number of sample events to report when providing cluster details  | Yes |
| reporting\_frequency | The frequency to report cluster analysis to streaming destinations  | Yes |

```go
cluster:
  name: clustering
  num_of_clusters: 100
  samples_per_cluster: 3
  reporting_frequency: 30s    
```

## Regexes - Simple Match

If enabled, the simple match regex processors will analyze incoming lines and automatically generate statistics, and detect anomalies based on the events that match the given match pattern.

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific processor, used for mapping this processor to a workflow | Yes |
| pattern | Regular Expression pattern to define which strings to match on | Yes |
| **trigger\_thresholds** | The trigger\_thresholds section is used to define trigger\_thresholds \(alerting and automation\) based on Edge Delta's analysis of the incoming data | Yes |
| anomaly\_probability\_percentage | The percent confidence level \(0 - 100\) that needs to be breached in order to generate a trigger. Lower values \(0-50\) will generate a trigger if minor anomalies are detected within the data, higher values \(50+\) will only generate a trigger if major anomalies are detected. Default value = 90 | No |
| upper\_limit\_per\_interval | Static threshold for generating a trigger, if the number of events that match the given pattern for the most recent reporting interval is greater than that limit, a trigger will be generated. No default value. | No |

```go
regexes:
  - name: "errors"
    pattern: "error|err|ERROR|ERR"
    trigger_thresholds:
      anomaly_probability_percentage: 90       
```

## Regexes - Statistical Capture

If enabled, the statistical capture regex processors will analyze a specific numerical field,  and automatically generate statistics and detect anomalies based on the aggregate values parsed out from the events. 

Typically Statistical Capture regexes are used for numerical statistics, such as response times, process times, sizes \(bytes, pool size, buffer, ...\), active users, etc.

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific processor, used for mapping this processor to a workflow | Yes |
| pattern | Regular Expression pattern containing a capture group to define which field to perform statistics on | Yes |
| **trigger\_thresholds** | The trigger\_thresholds section is used to define trigger\_thresholds \(alerting and automation\) based on Edge Delta's analysis of the incoming data | Yes |
| anomaly\_probability\_percentage | The percent confidence level \(0 - 100\) that needs to be breached in order to generate a trigger. Lower values \(0-50\) will generate a trigger if minor anomalies are detected within the data, higher values \(50+\) will only generate a trigger if major anomalies are detected. Default value = 90 | No |
| upper\_limit\_per\_interval | Static threshold for generating a trigger, if the number of events that match the given pattern for the most recent reporting interval is greater than that limit, a trigger will be generated. No default value. | No |

```go
regexes:
  - name: "response_time"
    pattern: "completed in (\\d+)ms"
    trigger_thresholds:
      anomaly_probability_percentage: 90
```

## Regexes - Dimension Counter

If enabled, the dimension counter regex processors will analyze incoming lines and dynamically generate the values for a given dimension. For each of the values of that dimension, the system will automatically generate statistics, and detect anomalies based on the events that match the given match pattern.

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific processor, used for mapping this processor to a workflow | Yes |
| pattern | Regular Expression pattern containing a named capture group, or set of named capture groups to define which field\(s\) to perform dimensional statistics on. _Note: named capture groups must follow Golang regex protocol, ex:  "status\_code=\(?P&lt;status\_code&gt;\d+\)"_ | Yes |
| **trigger\_thresholds** | The trigger\_thresholds section is used to define trigger\_thresholds \(alerting and automation\) based on Edge Delta's analysis of the incoming data | Yes |
| anomaly\_probability\_percentage | The percent confidence level \(0 - 100\) that needs to be breached in order to generate a trigger. Lower values \(0-50\) will generate a trigger if minor anomalies are detected within the data, higher values \(50+\) will only generate a trigger if major anomalies are detected. The anomaly\_probability\_percentage threshold will be applied dynamically to each underlying value found for the given dimension\(s\). Default value = 90 | No |
| upper\_limit\_per\_interval | Static threshold for generating a trigger, if the number of events that match the given pattern for the most recent reporting interval is greater than that limit, a trigger will be generated. The upper\_limit\_per\_interval threshold will be applied dynamically to each underlying value found for the given dimension\(s\). No default value. | No |

```go
regexes:
  - name: "log_levels"
    pattern: "level=(?P<log_level>\\w+) "
    trigger_thresholds:
      anomaly_probability_percentage: 90       
```

