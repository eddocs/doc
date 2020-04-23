# Configuration

The Edge Delta agents utilize a configuration file to manage various settings such as: Inputs \(Sources\), Rules \(Monitors and Analytics\) that it performs against the data, as well as Destinations \(Streaming and Triggers\).

The configuration file is automatically loaded into memory at runtime. Updates to the configuration file are typically made via the CCB \(Central Configuration Backend\), or locally against the file itself. 

If configuration updates are made in the UI, via the CCB, these updates are automatically propagated down to the agent, without requiring a restart. 

## Schema

The configuration file has three main parts:

| Name | Description |
| :--- | :--- |
| [Agent settings](https://docs.edgedelta.com/configuration/agent-settings) | Configure settings for Edge Delta agent, these settings apply to the whole configuration file |
| [Workflows](https://docs.edgedelta.com/configuration/workflows) | Configure inputs \(sources\) and outputs \(where you want Edge Delta agent to send results, and notifications\)  |
| [Monitors](https://docs.edgedelta.com/configuration/monitors) | Configure rules, regexes and triggers |



