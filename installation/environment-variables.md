---
description: >-
  This document outlines the environment variable parameters that can be passed
  in while installing and deploying the Edge Delta agent.
---

# Environment Variables

## Frequently Used Environment Variables

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ED_API_KEY</td>
      <td style="text-align:left">API Key used to pull agent&apos;s configuration details (generated via
        ED Admin Portal)</td>
      <td style="text-align:left">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</td>
      <td style="text-align:left">0a3a6ca3-0df0-45f8-8ea2-d1329ee3de60</td>
    </tr>
    <tr>
      <td style="text-align:left">ED_WORKFLOWS</td>
      <td style="text-align:left">Colon (:) separated workflow names that will enable all matching workflows
        and disable the rest together with ED_WORKFLOW_PREFIXES</td>
      <td style="text-align:left">name:name:...</td>
      <td style="text-align:left">
        <p>workflow_1:workflow_2</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ED_WORKFLOW_PREFIXES</td>
      <td style="text-align:left">Colon (:) separated workflow prefixes that will enable all matching workflows
        according their prefixes and disable the rest together with ED_WORKFLOWS</td>
      <td style="text-align:left">prefix:prefix:...</td>
      <td style="text-align:left">
        <p>workflow_prod_:workflow_cache_</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HTTP_PROXY</td>
      <td style="text-align:left">Proxy details for routing Edge Delta agent&apos;s outbound traffic through
        an HTTP internal proxy</td>
      <td style="text-align:left">domain:port</td>
      <td style="text-align:left">
        <p>http://127.0.0.1:3128</p>
        <p>127.0.0.1:3128</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS_PROXY</td>
      <td style="text-align:left">Proxy details for routing Edge Delta agent&apos;s outbound traffic through
        an HTTPs internal proxy</td>
      <td style="text-align:left">domain:port</td>
      <td style="text-align:left">
        <p>https://127.0.0.1:3128</p>
        <p>127.0.0.1:3128</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">NO_PROXY</td>
      <td style="text-align:left">Disable proxy for requests hitting a specific destination</td>
      <td style="text-align:left">domain:port</td>
      <td style="text-align:left">
        <p>https://your-endpoint.com</p>
        <p></p>
      </td>
    </tr>
  </tbody>
</table>

## Examples - Kubernetes (yml configuration)

Snippet pulled from: [https://edgedelta.github.io/k8s/edgedelta-agent.yml](https://edgedelta.github.io/k8s/edgedelta-agent.yml)

```yaml
spec:
  containers:
  - name: edgedelta
    image: docker.io/edgedelta/agent:latest
    env:
      - name: ED_API_KEY
        valueFrom:
          secretKeyRef:
            key: ed-api-key
            name: ed-api-key
      - name: HTTPS_PROXY
        value: <your proxy details>

```

Note that "ED_API_KEY" is not defined in the yaml as clear text. Using the Kubernetes secrets mechanism, secret value should be defined with below command within the Kubernetes cluster:
```bash
kubectl create secret generic ed-api-key --namespace=edgedelta --from-literal=ed-api-key="YOUR_API_KEY_VALUE"
```

## Examples - Linux/MacOSX

ED_ENV_VARS is a special variable used during installation where multiple environment variables specified in following comma separated format: "variable1=value1,variable2=value2"

```bash
sudo ED_API_KEY=<your api key> \
ED_ENV_VARS="HTTPS_PROXY=<your proxy details>" \
bash -c "$(curl -L https://release.edgedelta.com/release/install.sh)"
```
## Examples - Docker

```bash
docker run --rm -d --name edgedelta \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-e "ED_API_KEY=<your api key>" \
-e "HTTPS_PROXY=<your proxy details>" \
edgedelta/agent:latest

```

## Example - Windows

On Windows systems use following command to define environment variables globally. Agent service needs to be restart after setting the variable.

`[System.Environment]::SetEnvironmentVariable('HTTP_PROXY', '<your proxy details>',[System.EnvironmentVariableTarget]::Machine)`