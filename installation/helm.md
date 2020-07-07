---
description: >-
  The following document covers the process for deploying the Edge Delta agent as a DaemonSet on your Kubernetes cluster via helm charts.
  We are assuming you have conceptual understanding of helm charts. 
---

# Kubernetes

Edge Delta agent is a daemon that analyze logs and container metrics from a Kubernetes cluster and stream analytics to configured streaming destination. This page streamlined instructions to get you up and running in Kubernetes environment.

Edge Delta uses Kubernetes recommended node level logging architecture, in other words DaemonSet architecture. The DaemonSet runs Edge Delta agent pod on each node. Each Agent pod analyzes logs from all other pods running on the same node. 

## Installation

Add Edge Delta helm repository

```text
helm repo add edgedelta https://edgedelta.github.io/charts
```

Run Helm installation

```text
helm install edgedelta edgedelta/edgedelta --set apiKey=<API_KEY>
```

Output
```text
NAME: edgedelta
LAST DEPLOYED: Tue Jul 7 22:23:37 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. Visit https://admin.edgedelta.com
2. Find the configuration with <API_KEY> to check reporting status
```

Show helm installed packages 

```text
helm ls
```

## Useful Tips

### Uninstall helm chart

```text
helm delete edgedelta
```
