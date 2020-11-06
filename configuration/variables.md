---
description: >-
  This document describes usage of environment variables in Edge Delta configuration.
---

# Variables

## Overview

Edge Delta supports the usage of environment variables as values in configuration file. Variables are especially useful to pass secrets to agent in a secure manner.

Variables can be referred in one of the following formats:

```
{{ Env "MY_VARIABLE_NAME" }}
{{ Env "MY_VARIABLE_NAME" "my default value" }}
```

If no default value is provided existence of the variable in agent execution environment is expected. Otherwise agent will stop with error.

If default value is provided and variable does not exists on agent execution environment default value will be used.

## Example

Slack endpoint is a secret which contains the token for posting directly into a slack channel.

Instead of explicitly putting it into configuration it can be referred from agent execution environment as below:

```
  triggers:
      - name: slack-integration
        type: slack
        endpoint: {{ Env "MY_SLACK_ENDPOINT" }}
```
