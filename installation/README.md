---
description: >-
  The following document provides an overview for Installing the Edge Delta
  agent
---

# Installation

The Edge Delta installation package is available and fully supported for Windows, Linux, and MacOS operating systems. A Docker image is also available for containerized environments. Select from the following deployment types below to review the appropriate documentation:

* [Windows](windows.md)
* [Linux](linux.md)
* [MacOS](macos.md)
* [Docker](docker.md)

## Typical Installation Architecture

For a usual installation, the analysis initially starts at the agents, where raw logs, metrics, and telemetry is pre-processed and applied to both streams and triggers:

![Anomaly Captures, Analytics and Insights, and Alerts and Automation are all easily integrated.  ](../.gitbook/assets/image%20%283%29.png)

The agent analyzes all data in real time, where it then can feed the Anomaly Captures, Analytics and Insights, and Alerts and Automation into existing systems. 

The raw data on the other hand is forwarded to low cost storage solutions that still have re-ingestion, re-indexing, or dynamic searching capabilities. \(Snowflake, S3, Blob Storage, etc\).

