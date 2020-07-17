---
description: >-
  The following document covers the process for deploying the Edge Delta agent
  as a DaemonSet on your Kubernetes cluster via helm charts. We are assuming you
  have conceptual understanding of helm charts
---

# Kubernetes via Helm

Edge Delta agent is a daemon that analyze logs and container metrics from a Kubernetes cluster and stream analytics to configured streaming destination. This page streamlined instructions to get you up and running in Kubernetes environment.

Edge Delta uses Kubernetes recommended node level logging architecture, in other words DaemonSet architecture. The DaemonSet runs Edge Delta agent pod on each node. Each Agent pod analyzes logs from all other pods running on the same node.

## Installation

Add Edge Delta helm repository

```text
helm repo add edgedelta https://edgedelta.github.io/charts
```

Run Helm installation and create "edgedelta" namespace

```text
helm install edgedelta edgedelta/edgedelta --set apiKey=<API-KEY> -n edgedelta --create-namespace
```

Output

```text
NAME: edgedelta
LAST DEPLOYED: Fri Jul 17 17:49:42 2020
NAMESPACE: edgedelta
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. Visit https://admin.edgedelta.com
2. Find the configuration with <API-KEY> to check if agents are active
```

Show helm installed packages in "edgedelta" namespace

```text
helm ls -n edgedelta
```

## Useful Tips

### Uninstall helm chart

```text
helm delete edgedelta -n edgedelta
```
