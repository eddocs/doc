# Linux

The configuration file is loaded into memory at runtime and is used to both determine the inputs and the outputs of the Edge Delta agent. There is an example json that is included in the download package that you can use as a guide. Please do note that the config is not initially usable as it includes two invalid links as outputs.

The first part of the config is the "path" which defines the scope of where the Edge Delta agent will look.

For example:

```javascript
"path" : "C:\\EdgeDeltaPOCWork\\SB_SPC\\DataOutput.log"
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

