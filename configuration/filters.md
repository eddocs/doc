---
description: >-
  This document outlines the various Filters types supported by the Edge Delta
  agent, and how the filters are configured for inputs.
---

# Filters

## Overview

Filters can be used to filter and transform the received logs before further processing.
They are useful to discard unnecessary logs, protect sensitive data (e.g. mask ssn) and reduce the agent resource usage (due to less data being fed into processors), .

Filters are defined at top level in config yml and 

```yaml
  filters:
    - name: error
      type: regex
      pattern: "error"
```

Filters can be referred at different places based on need.
* Input filters apply right after the data ingestion from the input and before running workflows associated with the input.
* Workflow filters apply before running processors within the workflow.
* Processor filters apply before the processor runs regardless of which workflow the processor is running within.


### Regex Filters

Regex filters pass all log lines that match the specified regular expression for further processing and discard all unmatched logs.

Below example will grab the log lines that are error related and discard other lines.

```yaml
  - name: error
    type: regex
    pattern: "error|ERROR|ERR|Err"
```

Negative filters are also possibla via *negate* option.
Below example will discard any debugging information from the input source to focus on more important events:

```yaml
  - name: not_debug
    pattern: "Debug|DEBUG"
    negate: true
```

### Mask Filters

Mask filters transform the log lines to hide the matched part of the content for the given regex pattern.

Below example filter replaces "password: SOME_PASSWORD" with "password: \*\*\*\*\*\*":

```yaml
  - name: mask_password
    type: mask
    pattern: 'password:\s*\w+'
    mask: 'password: ******'
```

If mask is omitted, default mask \*\*\*\*\*\* will be applied. Specifying empty mask "" will simply remove matched the pattern from the log line.

Instead of defining a regex pattern it is also possible to use one of the predefined patterns.
Available predefined patterns are below:
* credit_card
* us_phone_dash

Below is an example filter that masks US phone numbers:

```yaml
  - name: mask_phone
    type: mask
    predefined_pattern: us_phone_dash
```

### Buffered trace filter

Buffered trace filter is a special purpose filter for trace logs. By "trace log" we mean a set of logs that can be tied together with an id such as trace id or request id. Buffered trace filter groups the logs by specified id, waits for a specified duration to make sure all relavant events of that trace/request is collected and then makes a decision on either discard the trace logs or pass them based on configuration.

Options are
- pass through failed operation events
- pass through high latency operation events
- pass through certain percentage of successful events

TODO: explain each field

```yaml
filters:
- name: trace_filter
  type: buffered-trace
  trace_id_pattern: \"trace_id\":\"(?P<id>\w+)"
  failure_pattern: \"status\":\"Failed\"
  latency_pattern: \"duration\":\"(?P<latency>\d+)\"
  latency_threshold: 8000
  trace_deadline: 1m
```

## Usage

Filter names are used to apply filters to inputs, workflows and processors. When multiple filters are provided they are applied in given order, from top to bottom.

* Below is an example file input with *error* and *mask_card* filters:

  ```yaml
    inputs:
      files:
        - labels: "billing"
          path: "/var/log/billing/*.log"
          filters:
            - error
            - mask_card
  ```
See [Inputs](https://docs.edgedelta.com/configuration/inputs) documentation for details about inputs that can be filtered.

* Below is an example workflow with *error* filter:

  ```yaml
  workflows:
    application_workflow:
      input_labels:
        - system_stats
        - agent_stats
        - application_logs
      filters:
        - error
      processors:
        - error-check
        - fail-check
        - success-check
      destinations:
        - sumo-logic-devops-integration
        - slack-devops-integration
  ```
See [Workflows](https://docs.edgedelta.com/configuration/workflows) documentation for details about workflows that can be filtered.

* Below is an example Dimension Counter Processor with *not_debug* filter.

  ```yaml
  regexes:
    - name: "log"
      pattern: "level=(?P<level>\\w+) "
      dimensions: ["level"]
      trigger_thresholds:
        anomaly_probability_percentage: 90
      filters:
        - not_debug
  ```

See [Processors](https://docs.edgedelta.com/configuration/processors) documentation for details about processors that can be filtered.
