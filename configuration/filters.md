---
description: >-
  This document outlines the various Filters types supported by the Edge Delta
  agent, and how the filters are configured for inputs.
---

# Filters

## Overview

Filters are the mechanism to filter and transform the received logs from input sources.

Proper filter configuration reduces resource usage, increases performance and hides or masks confidential data. It also provides a way to group the related events before further processing.

Filters apply right after the data ingestion from input and before any processing is done in the workflows associated with the input.

Filters should be defined at the top level, under filters section:

```go
  filters:
    - name: error
      type: regex
      pattern: "error"
```
Filter names are used to apply filters to inputs.

Below is an example file input with "error" and "mask_card" filters:

```go
  inputs:
    files:
      - labels: "billing"
        path: "/var/log/billing/*.log"
        filters:
          - error
          - mask_card
```
For details about inputs that can be filtered, review [Inputs](https://docs.edgedelta.com/configuration/inputs) documentation.

## Regex Filters

Regex filters pass all log lines that match the specified regular expression for further processing and discard unmatched logs.

Below example will grab log lines that ares error related and discard other lines.

```go
  - name: error
    type: regex
    pattern: "error|ERROR|ERR|Err"
```

Using negation it is possible to discard the specified content and process the rest.

Below example will discard any debugging information from the input source to focus on more important events:

```go
  - name: not_debug
    pattern: "Debug|DEBUG"
    negate: true
```

## Mask Filters

Mask filters transform the log lines to hide the matched part of the content for the given regex pattern.

An example that will replace any "password: SOME_PASSWORD" as "password: \*\*\*\*\*\*" is below:

```go
  - name: mask_password
    type: mask
    pattern: 'password:\s*\w+'
    mask: 'password: ******'
```

If mask is omitted, default mask "******" will be applied. Specifying empty mask "" will remove matched the pattern from the log line.

Instead of defining a regex pattern it is also possible to use a predefined pattern.

Below is an example filter masking US phone numbers in well known formats:

```go
  - name: mask_phone
    type: mask
    predefined_pattern: us_phone_dash
    mask: XXXXX
```

Available predefined patterns are below:
* credit_card
* us_phone_dash