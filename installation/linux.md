# Linux

Edge Delta provides a convenient self extracting installer package supporting common Linux distributions such as Ubuntu, Debian, CentOS, RHEL.

## Download

Contact Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to get a script URL and your API key.

## Installation

Replace the DOWNLOAD_URL below with the script URL you received from Edge Delta team and run following command in terminal:
```
ED_API_KEY=<YOUR_API_KEY> bash -c "$(curl -L <DOWNLOAD_URL>/install.sh)"

```

Script may prompt sudo password if you are not running it as root.

Script deploys Edge Delta into `path /opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

## Troubleshooting

Check the service status using one of the following commands depending on your distribution.

```text
service edgedelta status
systemctl status edgedelta
/etc/init.d/edgedelta status
```

Configuration path: `/opt/edgedelta/agent/conf.yaml`

Log file path: `/opt/edgedelta/agent/edgedelta.log`

