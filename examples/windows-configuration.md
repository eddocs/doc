---
description: >-
  The following document contains an example configuration for deployment on
  Linux-based Operating Systems
---

# Windows Configuration

Some of the sections in the example configuration are commented out \(starting with a "\#"\), or contain a field that needs to be added \(i.e. _"&lt;ADD SUMO LOGIC HTTPS ENDPOINT&gt;"_\). The goal is to provide a template to use as a starting point, however basic modifications are required to generate a working configuration.

Please comment/uncomment parameters as needed, as well as populate the appropriate values to create your desired configuration.

```go
#Configuration File Version (currently v1 and v2 supported)
version: v2

#Global settings to apply to the agent
agent_settings:         
  log:    
    level: info
  anomaly_capture_size: 250
  disable_printer: true

#Inputs define which datasets to monitor (files, containers, syslog ports, windows events, etc.)
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
#  files:
#    - labels: "iis_logs"
#      path: "C:\\inetpub\\Logs\\LogFiles\\W3SVC1\\*.log"
#  ports:
#    - labels: "syslog_ports"
#      protocol: tcp
#      port: 1514

#Outputs define destinations to send both streaming data, and trigger data (alerts/automation/ticketing)
outputs:

#Streams define destinations to send "streaming data" such as statistics, anomaly captures, etc. (Splunk, Sumo Logic, New Relic, Datadog, InfluxDB, etc.)
  streams:

#Sumo Logic Example
      - name: sumo-logic-integration
        type: sumologic
        endpoint: "<ADD SUMO LOGIC HTTPS ENDPOINT>"

#Splunk Example
#      - name: splunk-integration
#        type: splunk
#        endpoint: "<ADD SPLUNK HEC ENDPOINT>"
#        token: "<ADD SPLUNK TOKEN>"

#Datadog Example
#      - name: datadog-integration
#        type: datadog
#        api_key: "<ADD DATADOG API KEY>"

#New Relic Example
#      - name: new-relic-integration
#        type: newrelic
#        endpoint: "<ADD NEW RELIC API KEY>"

#Influxdb Example
#      - name: influxdb-integration
#        type: influxdb
#        endpoint: "<ADD INFLUXDB ENDPOINT>"
#        port: <ADD PORT>
#        features: all
#        tls: 
#          disable_verify: true
#        token: "<ADD JWT TOKEN>"
#        db: "<ADD INFLUX DATABASE>"

#Triggers define destinations for alerts/automation (Slack, PagerDuty, ServiceNow, etc)
  triggers:
      - name: slack-integration
        type: slack
        endpoint: "<ENTER SLACK WEBHOOK/APP ENDPOINT URL>"

#Processors define analytics and statistics to apply to specific datasets
processors:
#  cluster:
#      name: clustering
#      num_of_clusters: 50          # keep track of only top 100 clusters
#      samples_per_cluster: 2       # keep last 20 messages of each cluster
#      reporting_frequency: 30s     # report cluster samples every 30 seconds

#Regexes define specific keywords and patterns for matching, aggregation, statistics, etc. 
  regexes:
    # Error level Windows logs
    - name: "win_err"
      pattern: "{\"level\":\"error\"}"
      trigger_thresholds:
        anomaly_probability_percentage: 90
    # Critical Windows logs
    - name: "win_crit"
      pattern: "{\"level\":\"critical\"}"
      trigger_thresholds:
        anomaly_probability_percentage: 90
    # Windows Update Failure
    - name: "win_update_err"
      pattern: "{\"eventId\":20}"
      trigger_thresholds:
        anomaly_probability_percentage: 90
    # Windows Logon Failure
    # Enable via GPO or locally with windows CMD.exe: Auditpol /set /category:"Logon/Logoff" /Success:enable /failure:enable
    - name: "win_logon_fail"
      pattern: "{\"eventId\":4625}"
      trigger_thresholds:
        anomaly_probability_percentage: 90
    # Windows PowerShell
    - name: "win_ps_warn"
      pattern: "{\"level\":\"warning\"}"
      trigger_thresholds:
        anomaly_probability_percentage: 90

#Workflows define the mapping between input sources, which processors to apply, and which destinations to send the streams/triggers to
workflows:
  example_workflow:
    input_labels:
      - system_stats
      - agent_stats
      - windows_events
    processors:
      - win_err
      - win_crit
      - win_update_err
      - win_logon_fail
      - win_ps_warn
    destinations:
      - sumo-logic-integration
      - slack-integration
```

