---
title: Windows
weight: 1
---

# Getting Started

## What is Edge Delta?

In today's modern architectures, whether your infrastructure is physical, virtual, on-premise, in the cloud, containerized, or serverless applications and systems produce a large volume of logs, counters, metrics and information. Real-time analytics and stream processing are used to capture the current state of these systems and provide intelligent insight. This empowers teams to be able to observe, monitor, predict, alert, and remediate in an automated manner, ensuring uptime and availability of critical production systems.

Edge Delta has a novel approach to modern data analytics – the platform uses Federated Learning to analyze data. Utilizing data science concepts closest to where the data is created, Edge Delta intelligently pre-processes data before centralizing it, this unlocks unlimited data analysis, resulting in complete visibility and orders of magnitude faster alerting and automation.

![The Edge Delta platform is distributed, allowing analysis without the need to centralize raw data first](.gitbook/assets/image%20%2812%29.png)

## Typical Architecture

For a usual installation, the analysis initially starts at the agents, where raw logs, metrics, and telemetry is pre-processed and applied to both streams and triggers:



![Anomaly Captures, Insights, and Alerts and Automation, Raw Logs are all easily integrated.  ](.gitbook/assets/image%20%284%29.png)

The agent analyzes all data in real time, where it then can feed the Anomaly Captures, Analytics and Insights, and Alerts and Automation into existing systems. 

The raw data on the other hand is forwarded to low cost storage solutions that still have re-ingestion, re-indexing, or dynamic searching capabilities. \(Snowflake, S3, Blob Storage, etc\).

## Planning and Design

The Edge Delta agent is built with the ["Go" programming language](https://golang.org/), making it extremely performant, efficient and lightweight. The agent doesn't require installation \(but installers can also be used\) and runs as a background process. The Edge Delta Federated Learning backend can be supported on AWS, Azure, GCP, as well as On-prem if required. 

\(Typical\) If the agents have outbound internet connectivity, Edge Delta Central Configuration Backend \(CCB\) can be used to simplify configuration file changes especially in environments with many Edge Delta agents. CCB is a cloud service run by Edge Delta. Configuration files changes can be securely uploaded to this service, once uploaded, during runtime Edge Delta agents can pull the configuration file from the CCB service. More information how to configure CCB can be found under Configuration/Overview section below. 

\(Atypical\) If the agents do not have outbound internet connectivity, the Edge Delta agent works with a configuration file \(config.yaml\). Configuration file is used to configure the global settings for the agent, inputs \(sources\) used by the agent, monitors/rules performed by the agent, and the outputs where results are streamed.

In cases where there is no outbound internet connectivity, the configuration file is created automatically after installation and loaded into memory at runtime. After making changes to the `config.yaml` file, the changes are loaded on agent process restart. 



