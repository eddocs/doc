# Monitors

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

## 

