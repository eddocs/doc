# Windows 

## Configuration

Follow the directions below to run Edge Delta agent on Windows environments.

1. Download the [latest version](https://github.com/edgedelta/edgedelta-release) of the Edge Delta kit.
2. Create _C:\LogGenTest-CoffeeCo-SPC_ directory and copy the kit and agent contents there.
3. Run **Setup.cmd** \(this will simply create the _C:\EdgeDeltaPOCWork\SB\_SPC_ for logs output\).
4. Open **config\_windows.yaml**. Some example inputs and outputs have been pre-configured, modify these as needed. Both URLs at the end of config need to be updated with valid URLs. Please see below for information on config file.

## Package Contents

1. **Main \(folder\)**: Set of scripts that allows you to emulate the logs of a production system which Edge Delta will monitor.
2. **cmd\_ErrorGen folders**: Scripts to help generate loads on systems \(to be used for proof of concept or testing purposes\). 
3. **README \(md\)**: Document that explains how to setup the agent and sandbox environment
4. **Setup.cmd**: Script to generate folder structure.
5. **Config\_windows \(yaml\)**: Configuration file required by the agent and loaded into memory when agent process is started. Can include global agent settings, inputs \(e.g: logs\) and outputs \(e.g: Slack or Sumo Logic or other partners\)
6. **edgedelta\_\(msi\)**: Edge Delta agent. 

## Configuration File Instructions

The configuration file is loaded into memory at runtime and is used to both determine the inputs and the outputs of the Edge Delta agent. There is an example yaml that is included in the download package that you can use as a guide. Please do note that the config is not initially usable as it includes two invalid links as outputs.

The configuration file has three main parts:

1. Agent settings \(global\)

   Configure global settings for the Edge Delta agent.

2. Workflows

   Configure inputs \(sources\) and outputs \(where you want Edge Delta agent to send results, and notifications\) in this part.

3. Monitors

   Configure regexes and triggers in this part.

Now let's go into details of each part.

### Agent settings

Schema:

```javascript
agent_settings:
  agent_key: 
  ac_buffer_size: 
  tag: 
  disable_printer: 
  grace_period: 
  log:
    - level: 
    - path: 
```

| Setting | Required | Type | Options | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| agent\_key | Yes | GUID | GUID | N/A | Unique key that identifies Edge Delta agent for your company, given to you by the Edge Delta sales team.  |
| ac\_buffer\_size | No | Integer | 0-9999 |  | Defines the space the Edge Delta agent utilizes in memory in MB |
| tag | No | Text | 1-128 characters or numbers | N/A | User defined prefix that agent writes on each line that is sent to an output.  |
| disable\_printer | No | Boolean | true/false | false | Disables writing agent results on screen. By default it is enabled. |
| grace\_period | Yes | Time | 1-9999s | 0s | Grace period agent waits before triggering alerts. Can be in seconds \(s\), minutes \(m\) |
| log | No |  |  |  | If not specified, agent uses default name \(edgedelta.log\), default level \(error\) and default location \(path where agent ran\) |
| log/level | No | Text | error, warning, info |  | Logging level for the agent logs |
| log/path | No | Text |  | N/A | Path of the log file; if path is not specified, the log file is created  uses the path where the agent ran. |

Example:

```javascript
agent_settings:
  agent_key: 1234-A1B1-2345-1234
  ac_buffer_size: 125
  tag: QAServers
  disable_printer: true
  grace_period: 30s
  log:
    - level: error
    - path: e:\logs\myedgedelta.log
```

Will look within that directory and log file.

The second part of the config defines which data "metrics" will be analyzed.

For example:

```javascript
"metrics": 
[
    {
        "name": "ERROR",
        "pattern": "\\sERROR",
        "window_size_in_min": 1, 
        "alert_threshold_for_anomaly": 90
    }
]
```

Will look for a space followed by the string "ERROR", will keep long term data histograms with 1 minute sizes, and will trigger alert conditions when the anomaly score exceeds 90.

```javascript
{
    "name": "RESPONSE_TIME_MS",
    "pattern": "Response time (?P<time>\\d+)",
    "window_size_in_min": 1, 
    "alert_threshold_for_anomaly": 90
}
```

Will look for a response time, pull a specific metric out of the logs \(in this case a ms response time\), and again trigger alert conditions when the anomaly score exceeds 90.

Next, there is the option to add a "traces" section that allows you to look for a specific process.

For example:

```javascript
"traces": 
[
    {
        "name": "Order",
        "start_pattern": "Example request to the Orders queue: (?P<OrderId>[0-9]+)",
        "finish_pattern": "Example order is completed: (?P<OrderId>[0-9]+)",
        "alert_threshold_in_ms": 12000

    }
]
```

Will alert when it sees a specific OrderId that exceeds a specified maximum allowable timeframe.

The final section of the config "pusher" defines where you can stream data or alerts

For example:

```javascript
"pusher": 
[
    {
        "name": "sumoLogic",
        "url": "https://endpoint4.collection.us2.sumologic.com/receiver/v1/http/restOfURL0001"
    },
    {
        "name": "slack",
        "url": "https://hooks.slack.com/services/restOfURL0001/restOfURL0002/restOfURL0003"
    }
]
```

Will stream all anomaly statistics to Sumo Logic for dashboarding or historical trending purposes. In addition, any environment that meets an alert condition will trigger an alert to be sent to a Slack channel.

 **Note**  
This example uses Sumo Logic as the analytics platform but Edge Delta feeds intelligence, statistics and alerts to many other platforms. Check [Edge Delta web site](https://edgedelta.com/) for list of all current integrations. 

## Running Edge Delta

1. Run _C:\LogGenTest-CoffeeCo-SPC\Main\RunSB\_SPC\_POC\_B+R.cmd_
2. Run _C:\LogGenTest-CoffeeCo-SPC\EdgeDelta.exe_
3. OPTIONAL: _Run C:\LogGenTest-CoffeeCo-SPC\main\RunSB\_SPC\_POC\_Errors\_PRODISSUE.cmd_ to emulate an increase in errors as would occur durring a production/site issue

## Expected Results

At this point, if you've completed the steps above, you should be able to see the agent running in the console. Using primarily in-memory computing, the Edge Delta agent calculates various statistics \(max, min, P90, P95, P99, avg, stddev...\) and learns specific metrics within the environment over time. After sufficient data has been analyzed to baseline the environment \(this should be accomplished in under 5 minutes\), the anomaly score will be accurately calculated to indicate the certainty level that the Edge Delta platform is detecting an anomaly \(scores closer to 0 are normal/expected behavior and scores closer to 100 are anomalies/unexpected\).

When the score passes the anomaly threshold, alerting actions \(eg: Slack alerts\) are triggered. If you completed _Optional Step 3_ under _Running Edge Delta_ section above, this should have triggered an anomaly to be detected.

KERIMH: ADD MORE INFO ABOUT NEW ANOMALY BEHAVIOR

For any additional information or questions, please email [info@edgedelta.com](mailto:info@edgedelta.com)

