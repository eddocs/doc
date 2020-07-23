---
description: >-
  The following document covers the process for deploying the Edge Delta agent
  as a DaemonSet on your Kubernetes cluster. We are assuming you have conceptual
  understanding of Kubernetes such as Pods, No
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

Once you have the name of the pod running the Edge Delta Agent, run below command to see Edge Delta agent logs;

```text
kubectl logs <pod_name> -n edgedelta
```

## Useful Tips

### Uninstall Edge Delta DaemonSet

```text
kubectl delete daemonset edgedelta --namespace edgedelta
```

### Running Edge Delta agent on select nodes

To run Edge Delta Agent on specific nodes of your cluster, add a node selector or nodeAffinity section to your pod config file. If your desired nodes are labeled logging=edgedelta then adding following nodeSelector will restrict Edge Delta agent pods to Nodes that have logging=edgedelta label.

```text
spec:
  nodeSelector:
    logging: edgedelta
```

Read more about specifying [node selectors and affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/).

### SELinux & Openshift

If you are running a SELinux enforcing Kubernetes cluster you need to add following securityContext configuration into edgedelta-agent.yml manifest DaemonSet spec. This change will run agent pod in privileged mode to allow collecting logs of other pods.

```text
     runAsUser: 0
     privileged: true
```

In an OpenShift cluster you need to also run below commands to allows agent pods to run in privileged mode.

```text
oc-test oc adm policy add-scc-to-user privileged system:serviceaccount:edgedelta:edgedelta
oc-test oc patch namespace edgedelta -p \
'{"metadata": {"annotations": {"openshift.io/node-selector": ""}}}'
```

### Output to cluster services in other namespaces

Edge Delta pods run in dedicated edgedelta namespace. If you desire to configure an output destination within your Kubernetes cluster make sure to set a resolvable service endpoint in your agent configuration.

Example: If you have an Elasticsearch service "elasticsearch-master" in "elasticsearch" namespace with port 9200 in your cluster "cluster-domain.example" you need to specify elastic output address as below in agent configuration:

```text
  address:
       - http://elasticsearch-master.elasticsearch.svc.cluster-domain.example:9200
```

Read more about [service DNS resolution](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#a-aaaa-records)

