---
description: >-
  This document outlines the various Input types supported by the Edge Delta
  agent, and how the inputs are configured.
---

# Inputs

## Overview

Inputs are the mechanism that tells the Edge Delta agent which data types for it to listen to, their location or configuration, as well as associated tags. 

The labels are used to map inputs to specific monitoring rules, or streaming and alerting destinations.

## Agent Stats

If enabled, Agent Stats will report agent level metrics, such as lines analyzed, bytes analyzed, etc.

```go
  agent_stats:
    enabled: true
    labels: "agent_stats"
```

## System Stats

If enabled, System Stats will report host level metrics, such as CPU, Memory, Disk, etc. for the host the agent is deployed on.

```go
  system_stats:
    enabled: true
    labels: "system_stats"
```

## Container Stats \(Docker\)

If enabled, Container Stats will report container level metrics, such as CPU, Memory, Disk, etc. for each container running on the host.

```go
 container_stats:
    enabled: true
    labels: "docker_stats"
```

## Files

If enabled, Files allows you to specify a set of files to have monitored by the Edge Delta service.

```go
  files:
    - path: "/var/log/service_a.log"
      labels: "app,service_a"
    - path: "/var/log/service_b.log"
      labels: "app,service_b"
    - path: "/var/log/apache2.access.log"
      labels: "web,apache"

```

## Ports

If enabled, Ports allows you to specify a set of ports and protocols to have the agent listen on for incoming traffic.

```go
  ports:
    - protocol: tcp
      port: 514
      labels: "syslog,firewall"
    - protocol: udp
      port: 1514
      labels: "syslog,router"
    - protocol: tcp
      port: 8080
      labels: "syslog,tls,service_a"
      tls:
        crt_file: /certs/server-cert.pem
        key_file: /certs/server-key.pem
        ca_file: /certs/ca.pem
```

## Windows Events

If enabled, Windows Events allows you to specify a set of Windows Events channels to be monitored by the Edge Delta service.

```go
  winevents:
    - channel: "Application"
      labels: "win_events,application"
    - channel: "Security"
      labels: "win_events,security"
    - channel: "System"
      labels: "win_events,system"
    - channel: "Microsoft-Windows-Sysmon/Operational"
      labels: "win_events,sysmon"

```

## Containers

If enabled, Containers allows you to specify a set of Docker Containers to be monitored by the Edge Delta service.

Note: In the 'include' section, after "image=" this is a contains match, so as long as the value provided is contained anywhere in the image name, the value will match. 

```go
  containers:
    - include:
        - "image=.*"
      labels: "docker, all_containers"
    - include:
        - "image=nginx:latest"
      labels: "docker, nginx"

```

## Examples - Linux

```go
inputs:
  system_stats:
    labels: "system_stats"
  agent_stats:
    labels: "agent_stats"
  files:
    - labels: "system_logs, auth"
      path: "/var/log/auth.log"
    - labels: "system_logs, syslog"
      path: "/var/log/syslog"
    - labels: "system_logs, secure"
      path: "/var/log/secure"
    - labels: "system_logs, messages"
      path: "/var/log/messages"
  ports:
    - labels: "syslog_tcp_ports"
      protocol: tcp
      port: 1514
    - labels: "syslog_tcp_ports"
      protocol: tcp
      port: 514
    - labels: "syslog_udp_ports"
      protocol: udp
      port: 1514
    - labels: "syslog_udp_ports"
      protocol: udp
      port: 514
```

## Examples - Windows

```go
inputs:
  system_stats:
    labels: "system_stats"
  agent_stats:
    labels: "agent_stats"
  winevents:
    - labels: "windows_events, application"
      channel: "Application"
    - labels: "windows_events, security"
      channel: "Security"
    - labels: "windows_events, system"
      channel: "System"
  files:
    - labels: "iis_logs"
      path: "C:\\inetpub\\Logs\\LogFiles\\W3SVC1\\*.log"
  ports:
    - labels: "syslog_tcp_ports"
      protocol: tcp
      port: 1514
    - labels: "syslog_udp_ports"
      protocol: udp
      port: 514
```

## Examples - Docker

```go
inputs:
  system_stats:
    enabled: true
    labels: "system_stats"
  container_stats:
    enabled: true
    labels: "container_stats"
  agent_stats:
    enabled: true
    labels: "agent_stats"
  containers:
    - labels: "docker_logs,all_containers"
      include:
        - "image=.*"
```

