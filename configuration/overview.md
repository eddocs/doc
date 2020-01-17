# Overview

The configuration file is loaded into memory at runtime and is used to both determine the inputs and the outputs of the Edge Delta agent. There is an example yaml that is included in the download package that you can use as a guide. Please do note that the config is not initially usable as it includes two invalid links as outputs.

The configuration file has three main parts:

| Name | Description |
| :--- | :--- |
| Agent settings | Configure settings for Edge Delta agent, these settings apply to the whole configuration file |
| Workflows | Configure inputs \(sources\) and outputs \(where you want Edge Delta agent to send results, and notifications\)  |
| Monitors | Configure regexes and triggers |

### Example Configuration File

