# Linux

Edge Delta provides a convenient self extracting installation package supporting common Linux distributions such as Ubuntu, Debian, CentOS, RHEL. 

## Download

Contact the Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to create an account and get access to the agent deployment portal. 

## Installation

Update the &lt;YOUR\_API\_KEY&gt; field with your configuration API Key from the administration portal: 

![](../.gitbook/assets/screen-shot-2020-03-31-at-1.16.15-pm.png)

Replace the DOWNLOAD\_URL string below with the endpoint URL you received from the Edge Delta team.

```text
ED_API_KEY=<YOUR_API_KEY> bash -c "$(curl -L <DOWNLOAD_URL>/install.sh)"
```

The installation process may prompt for the sudo password if you are not running as root. 

The installation process deploys Edge Delta into the path`/opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

## Troubleshooting

Check the service status using one of the following commands depending on your distribution.

```text
service edgedelta status
systemctl status edgedelta
/etc/init.d/edgedelta status
```

Configuration File path: `/opt/edgedelta/agent/config.yaml`

Edge Delta's Service Log file path: `/opt/edgedelta/agent/edgedelta.log`

