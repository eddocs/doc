---
description: >-
  This document outlines the process of defining Workflows within an Edge Delta
  configuration.
---

# Workflows

## Overview

Workflows are the mapping of Inputs, Processors and Outputs, logically grouped together based on the underlying use-cases and analytics being performed.

## Workflow Definition

| Key | Description | Required |
| :--- | :--- | :--- |
| name | User defined name of this specific workflow. The workflow names are strictly used for labeling and organizing workflows within a configuration, thus are not reported to any destinations.  | Yes |
| input\_labels | A list of input labels to apply the given workflow to. Input labels are defined as part of the Input configuration.  | Yes |
| processors | A list of processor names to apply the given workflow to. Processor names are defined as part of the Processor configuration.  | Yes |
| destinations | A list of destinations \(Outputs\) to apply the given workflow to. Destination names are defined as part of the Output configuration.  | No |

```go
workflows:
  application_workflow:
    input_labels:
      - system_stats
      - agent_stats
      - application_logs
    processors:
      - error-check
      - fail-check
      - success-check
    destinations:
      - sumo-logic-devops-integration
      - slack-devops-integration
      
  security_workflow:
    input_labels:
      - syslog_traffic
      - windows_events
      - auth_logs
    processors:
      - traffic-patterns
      - authentication-monitoring
      - system-patterns
    destinations:
      - sumo-logic-security-integration
      - slack-security-integration         
```

