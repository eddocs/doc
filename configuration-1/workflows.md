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
| name | User defined name of this specific Workflow. The Workflow names are strictly used for labeling and organizing Workflows within a configuration, thus are not reported to any Destinations.  | Yes |
| input\_labels | A list of Input labels to apply to the given workflow. Input labels are defined as part of the Input configuration.  | Yes |
| processors | A list of Processor names to apply to the given Workflow. Processor names are defined as part of the Processor configuration.  | Yes |
| destinations | A list of Output names to apply to the given Workflow. Destination names are defined as part of the Output configuration.  | No |

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

