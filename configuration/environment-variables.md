---
description: >-
  This document outlines the environment variable parameters that can be passed
  in while installing and deploying the Edge Delta agent.
---

# Environment Variables

## Environment Variables

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

## Examples - Linux

```text
ED_API_KEY=<your api key> \
HTTPS_PROXY=<your proxy details> \
bash -c "$(curl -L https://release.edgedelta.com/release/install.sh)"

```

## Examples - Docker

```text
docker run --rm -d --name edgedelta \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-e "ED_API_KEY=<your api key>" \
-e "HTTPS_PROXY=<your proxy details>" \
edgedelta/agent:latest

```

## Examples - Kubernetes \(yml configuration\)

Snippet pulled from: [https://edgedelta.github.io/k8s/edgedelta-agent.yml](https://edgedelta.github.io/k8s/edgedelta-agent.yml)

```text
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

