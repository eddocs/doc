---
description: >-
  This document outlines the various Filters types supported by the Edge Delta
  agent, and how the filters are configured for inputs.
---

# Filters

## Overview

Filters can be used to filter and transform the received logs before further processing.
They are useful to discard unnecessary logs, protect sensitive data (e.g. mask ssn) and reduce the agent resource usage (due to less data being fed into processors), .

Filters are defined at the top level in config yml and 

```yaml
filters:
  - name: error
    type: regex
    pattern: "error"
```

Once defined, filters can be referred at different places in the config yaml.
* Input filters apply right after the data ingestion from the input and before running workflows associated with the input.
* Workflow filters apply before running processors within the workflow.
* Processor filters apply before the processor runs regardless of which workflow the processor is running within.


### Regex Filters

Regex filters pass all log lines that match the specified regular expression for further processing and discard all unmatched logs.

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific filter, used for referring this filter in inputs/processors/workflows | Yes |
| type | Default filter type is 'regex'  | No |
| pattern | Regular expression pattern to define which strings to match on  | Yes |
| negate | Can be set to 'true' to reverse the effect of filter  | No |



Below example will grab the log lines that are error related and discard other lines.

```yaml
  - name: error
    type: regex
    pattern: "error|ERROR|ERR|Err"
```

Negative filters are also possibla via *negate* option.
Below example will discard DEBUG logs and only pass thru other logs:

```yaml
  - name: not_debug
    pattern: "  DEBUG "
    negate: true
```


### Mask Filters

Mask filters transform the log lines to hide the matched part of the content for the given regex pattern. If is useful to mask sensitive data such as phone numbers, social securit numbers, credit card numbers etc.

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific filter, used for referring this filter in inputs/processors/workflows | Yes |
| type | Type should be set to "mask" to define a mask filter  | Yes |
| pattern | Regular expression pattern to define which strings to match on. Either *pattern* or *predefined_pattern* must be set. | No |
| predefined_pattern | There are some commonly used patterns predefined which can be used instead of custom pattern. Available predefined patterns are *credit_card* and *us_phone_dash* | No |
| mask | String to be used as replacement for the matched part of the log. Default mask is "\*\*\*\*\*\*". Specifying empty mask "" will simply remove matched the pattern from the log line | No |


Below example filter replaces "password: SOME_PASSWORD" with "password: \*\*\*\*\*\*":

```yaml
  - name: mask_password
    type: mask
    pattern: "password:\s*\w+"
    mask: "password: ******"
```

Instead of defining a regex pattern, it is also possible to use one of the predefined patterns.


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

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific filter, used for referring this filter in inputs/processors/workflows | Yes |
| trace_id_pattern | Regular expression pattern which is used to extract the trace id values ffrom logs. Must be a regex with single capture group | Yes |
| failure_pattern | Regular expression pattern whose match indicates that the trace event (group of logs sharing same id) is a failure. Failures are passed thru from this filter.  | Yes |
| trace_deadline | A [golang duration](https://golang.org/pkg/time/#ParseDuration) string that represents the max duration of a trace. Once the specified trace deadline reached the buffered trace filter takes all events belonging to the same trace, applies filters/sampling (based on configuration), and then if passed the events are passed thru | Yes |
| success_sample_rate | The sample rate [0,1] of successfull traces. Default is zero which means successfull traces are discarded. If it's set to 0.2 then 20% of successfull traces will pass thru this filter. *Note:* Any trace event without a failure_pattern match indicates successful trace.  | No |
| latency_pattern | Regular expression pattern which is used to extract the latency value (if applicable) from the trace logs. Must be a regex with single numeric capture group. Only one of the logs belonging to the same trace (sharing same id) should have such latency information or the last one will be picked to represent the latency of the trace. Once the latency value is extracted and converted to a number it can be used in conjunction with *latency_threshold* to pass thru high latency traces. This is useful to collect the high latency traces in addition to the failed ones which are already pass thru as described in *failure_pattern*.  | No |
| latency_threshold | A numeric value representing threshold for high latency limit. Latency of a trace is extracted using latency_pattern | No |



```yaml
filters:
- name: trace_filter
  type: buffered-trace
  trace_id_pattern: \"trace_id\":\"(?P<id>\w+)"
  failure_pattern: \"status\":\"Failed\"
  trace_deadline: 1m
  success_sample_rate: 0.0
  latency_pattern: \"duration\":\"(?P<latency>\d+)\"
  latency_threshold: 8000
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
