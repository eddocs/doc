---
description: >-
  This document outlines the various Filters types supported by the Edge Delta
  agent, and how the filters are configured for inputs.
---

# Filters

## Overview

Filters are the mechanism to filter and transform the received logs before further processing.

Proper filter configuration reduces resource usage, increases performance and protects confidential data.

Filters are usable at different phases of data ingestion and processing:
* Input filters apply right after the data ingestion from the input and before running workflows associated with the input.
* Workflow filters apply before running processors within the workflow.
* Processor rule filters apply before the processor runs.

## Definition

Filters should be defined at the top level, under filters section before using:

```yaml
  filters:
    - name: error
      type: regex
      pattern: "error"
```
### Regex Filters

Regex filters pass all log lines that match the specified regular expression for further processing and discard all unmatched logs.

Below example will grab the log lines that are error related and discard other lines.

```yaml
  - name: error
    type: regex
    pattern: "error|ERROR|ERR|Err"
```

Using negation it is possible to discard the specified content and process the rest.

Below example will discard any debugging information from the input source to focus on more important events:

```yaml
  - name: not_debug
    pattern: "Debug|DEBUG"
    negate: true
```

### Mask Filters

Mask filters transform the log lines to hide the matched part of the content for the given regex pattern.

An example that will replace any "password: SOME_PASSWORD" as "password: \*\*\*\*\*\*" is below:

```yaml
  - name: mask_password
    type: mask
    pattern: 'password:\s*\w+'
    mask: 'password: ******'
```

If mask is omitted, default mask \*\*\*\*\*\* will be applied. Specifying empty mask "" will remove matched the pattern from the log line.

Instead of defining a regex pattern it is also possible to use a predefined pattern.

Below is an example filter masking US phone numbers in well known formats:

```yaml
  - name: mask_phone
    type: mask
    predefined_pattern: us_phone_dash
    mask: XXXXX
```

Available predefined patterns are below:
* credit_card
* us_phone_dash

## Usage

Filter names are used to apply filters to inputs, workflows and processors. When multiple filters are provided they are applied in given order, from top to bottom.

* Below is an example file input with "error" and "mask_card" filters:

  ```yaml
    inputs:
      files:
        - labels: "billing"
          path: "/var/log/billing/*.log"
          filters:
            - error
            - mask_card
  ```
  For details about inputs that can be filtered, review [Inputs](https://docs.edgedelta.com/configuration/inputs) documentation.

* Below is an example workflow with "error" filter:

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
  For details about workflows that can be filtered, review [Workflows](https://docs.edgedelta.com/configuration/workflows) documentation.

* Below is an example workflow with "not_debug" filter:

  ```yaml
  regexes:
    - name: "log_levels"
      pattern: "level=(?P<log_level>\\w+) "
      dimensions: ["log_level"]
      trigger_thresholds:
        anomaly_probability_percentage: 90
      filters:
        - not_debug
  ```
  For details about processors that can be filtered, review [Processors](https://docs.edgedelta.com/configuration/processors) documentation.
