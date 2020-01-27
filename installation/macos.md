# MacOS

Edge Delta provides a convenient self extracting installer package for MacOS

## Download and installation

Edge Delta sales team will provide you the download URL. Replace download_link with given URL and run following commands in an empty folder.

```
wget download_link -v
chmod +x edgedelta_*_linux_amd64.sh
sudo ./edgedelta_*_linux_amd64.sh
```

Script deploys Edge Delta into path `/opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

You may check the service status using one of the following command:
```
launchctl list edgedelta
```

Configuration path is /opt/edgedelta/agent/conf.yaml

Log file paths is /opt/edgedelta/agent/conf.yaml
