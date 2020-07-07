---
description: >-
  The following document covers the process for deploying the Edge Delta agent as a DaemonSet on your Kubernetes cluster.
  We are assuming you have conceptual understanding of Kubernetes such as Pods, Nodes, DaemonSets etc. 
---

# Kubernetes

Edge Delta agent is a daemon that analyze logs and container metrics from a Kubernetes cluster and stream analytics to configured streaming destination. This page streamlined instructions to get you up and running in Kubernetes environment.

Edge Delta uses Kubernetes recommended node level logging architecture, in other words DaemonSet architecture. The DaemonSet runs Edge Delta agent pod on each node. Each Agent pod analyzes logs from all other pods running on the same node. 

## Installation

Create kubernetes namespace

```text
kubectl create namespace edgedelta
```

Create a kube secret that contains your api token.

```text
kubectl create secret generic ed-api-key \
	--namespace=edgedelta \
	--from-literal=ed-api-key="(log in to view API tokens)"
```

Create daemonset 

```text
kubectl apply -f https://edgedelta.github.io/k8s/edgedelta-agent.yml
```

Checking status of Edge Delta container

```text
kubectl get pods --namespace=edgedelta
```

Once you have the name of the pod running the Edge Delta Agent, use the following command:

```text
kubectl exec <pod_name> -- edgedelta status -v

```

## Useful Tips

### Running Edge Delta agent on select nodes
To run Edge Delta Agent on specific nodes of your cluster, add a node selector or nodeAffinity section to your pod config file. If your desired nodes are labeled logging=edgedelta then adding following nodeSelector will restricy Edge Delta agent pods to Nodes that have logging=edgedelta label.


```text
spec:
  nodeSelector:
    logging: edgedelta
```

Read more about specifying [node selectors and affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/).