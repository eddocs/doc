# MacOS

Edge Delta provides a convenient self extracting installer package for MacOS.

## Download

Contact Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to get a download link.

## Installation

Replace the DOWNLOAD\_URL below with the script URL you received from Edge Delta team and run following command in terminal:

```text
ED_API_KEY=<YOUR_API_KEY> bash -c "$(curl -L <DOWNLOAD_URL>/install.sh)"
```

Script may prompt sudo password if you are not running it as root.

Script deploys Edge Delta into path `/opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

## Troubleshooting

Check the service status using the following command

```text
launchctl list edgedelta
```

Configuration path: `/opt/edgedelta/agent/conf.yaml`

Log file path: `/opt/edgedelta/agent/edgedelta.log`

