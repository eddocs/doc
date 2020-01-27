# MacOS

Edge Delta provides a convenient self extracting installer package for MacOS.

## Download and installation

Contact Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to get a download link. Replace `download_link` below with the URL received from Edge Delta team and run following command in an empty folder.

```text
wget download_link -v
chmod +x edgedelta_*_linux_amd64.sh
sudo ./edgedelta_*_linux_amd64.sh
```

Script deploys Edge Delta into path `/opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

Check the service status using the following command

```text
launchctl list edgedelta
```

Configuration path is `/opt/edgedelta/agent/conf.yaml`

Log file path is `/opt/edgedelta/agent/edgedelta.log`

