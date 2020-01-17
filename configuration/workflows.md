# Workflows

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

