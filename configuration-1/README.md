# Configuration

Edge Delta agent works with a configuration file `config.yaml`. Configuration file is where you configure the global settings for the agent, inputs \(sources\) that the agent listens to, monitors/rules that it performs and the outputs that it sent its results.

The configuration file is loaded into memory at runtime. After making changes to the `config.yaml` file, agent process needs to be restarted so that agent can run with the new changes. 

## Schema

The configuration file has three main parts:

| Name | Description |
| :--- | :--- |
| [Agent settings](https://docs.edgedelta.com/configuration/agent-settings) | Configure settings for Edge Delta agent, these settings apply to the whole configuration file |
| [Workflows](https://docs.edgedelta.com/configuration/workflows) | Configure inputs \(sources\) and outputs \(where you want Edge Delta agent to send results, and notifications\)  |
| [Monitors](https://docs.edgedelta.com/configuration/monitors) | Configure rules, regexes and triggers |



