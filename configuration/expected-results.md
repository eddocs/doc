# Expected Results

## Expected Results

At this point, if you've completed the steps above, you should be able to see the agent running in the console. Using primarily in-memory computing, the Edge Delta agent calculates various statistics \(max, min, P90, P95, P99, avg, stddev...\) and learns specific metrics within the environment over time. After sufficient data has been analyzed to baseline the environment \(this should be accomplished in under 5 minutes\), the anomaly score will be accurately calculated to indicate the certainty level that the Edge Delta platform is detecting an anomaly \(scores closer to 0 are normal/expected behavior and scores closer to 100 are anomalies/unexpected\).

When the score passes the anomaly threshold, alerting actions \(eg: Slack alerts\) are triggered. If you completed _Optional Step 3_ under _Running Edge Delta_ section above, this should have triggered an anomaly to be detected.

For any additional information or questions, please email [info@edgedelta.com](mailto:info@edgedelta.com)

