---
description: >-
  The following document outlines the high level steps for an initial onboarding
  and deployment of the Edge Delta service.
---

# Basic Onboarding

## Create An Edge Delta Account

1. Navigate to [admin.edgedelta.com](https://admin.edgedelta.com/)
2. At the bottom of the Sign-In dialog, hit the _**Sign up**_ button to start the process
3. Once you have completed all of the steps for signing up, your account will automatically be created

## Create The Initial Configuration

1. Sign into [admin.edgedelta.com](https://admin.edgedelta.com/)
2. Navigate to the **Home** tab of the Edge Delta service
3. Identify the appropriate example configuration to use as a starting point based on the OS \(Docker, Linux, MacOS, or Windows\) of the server Edge Delta will be deployed on
4. Hit the **Edit** button for the appropriate configuration. Output \(below\) typically needs to be configured to ensure connection to other services. 
5. Scan the configuration and identify parameters that may need to change:
   1. **Inputs** section, add/remove/uncomment inputs as seen fit \(see [Inputs](https://docs.edgedelta.com/configuration/inputs) documentation for more details\)
   2. **Outputs** section, uncomment/add/remove outputs as seen fit \(see [Outputs](https://docs.edgedelta.com/configuration/outputs) documentation for more details\)
   3. **Processors** section, add/remove processors as seen fit \(see [Processors](https://docs.edgedelta.com/configuration/processors) documentation for more details\)
   4. **Workflows** section, update example\_workflow to match the labels and names of the Inputs, Outputs, and Processors defined within the configuration \(see [Workflows](https://docs.edgedelta.com/configuration/workflows) documentation for more details\)
6. Once the appropriate updates have been made to the configuration, hit the **Save** button in the bottom right corner of the editor

## Deploy

1. Identify the appropriate configuration you would like to use for deployment \(modified in prior step\)
2. Hit the **Deploy** button on the right-hand side of the configuration
3. **Copy** the appropriate deployment command \(based on the OS of the server Edge Delta will be deployed\)
4. Run the deployment command on the target server to deploy Edge Delta
   1. Docker, Linux, and MacOS: paste and run the command in terminal 
   2. Windows: Open Powershell and paste and run the command
5. If there are any issues appear after deploying the agent, view troubleshooting section for given OS of agent deployment \(see [Installation](https://docs.edgedelta.com/installation) documentation, select appropriate OS, and navigate to _**Troubleshooting**_ section of documentation\)

## Verify Successful Deployment

1. Log in to the configured Streaming Destination \(Output\) platform \(i.e. Splunk, Sumo Logic, Datadog, New Relic, etc.\)
2. Once logged into the appropriate platform, identify the appropriate source metadata to query for incoming Edge Delta data \(this source should match the source configuration details provided in the configuration file \(i.e. HTTPs Endpoint, HEC endpoint, API URL, etc.\)
3. Query the source that is configured to receive incoming Edge Delta data
4. Review query results. Incoming data should contain metadata tags that match the labels and tags defined in the configuration file

