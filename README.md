---
title: Windows
weight: 1
---

# Getting Started

## What is Edge Delta?

Edge Delta has a novel approach to modern data analytics – the platform uses Federated Learning to analyze data. Utilizing data science concepts closest to where the data is created, Edge Delta intelligently pre-processes data before centralizing it, this unlocks unlimited data analysis, resulting in complete visibility and orders of magnitude faster alerting and automation.

## Planning and Design

Edge Delta is built with the ["Go" programming language](https://golang.org/), it is extremely performant, efficient and lightweight. The agent doesn't require installation and runs as a background process.

Edge Delta agent works with a configuration file \(config.yaml\). Configuration file is where you configure the global settings for the agent, inputs \(sources\) that the agent listens to, monitors/rules that it performs and the outputs that it sent its results.

The configuration file is created automatically after installation and loaded into memory at runtime. After making changes to the `config.yaml` file, agent process needs to be restarted so that agent can run with the new changes. 

If your agents have internet connectivity, Edge Delta Central Configuration Backend \(CCB\) can be used to simplify configuration file changes especially in environments with many Edge Delta agents. CCB is a cloud service run by Edge Delta. You can securely upload your configuration file changes to this service, once uploaded, during runtime Edge Delta agents can pull the configuration file from the CCB service. More information about how to configure CCB can be found under Configuration/Overview section below.

