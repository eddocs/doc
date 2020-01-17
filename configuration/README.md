# Configuration

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

## Running Edge Delta

1. Run _C:\LogGenTest-CoffeeCo-SPC\Main\RunSB\_SPC\_POC\_B+R.cmd_
2. Run _C:\LogGenTest-CoffeeCo-SPC\EdgeDelta.exe_
3. OPTIONAL: _Run C:\LogGenTest-CoffeeCo-SPC\main\RunSB\_SPC\_POC\_Errors\_PRODISSUE.cmd_ to emulate an increase in errors as would occur durring a production/site issue



