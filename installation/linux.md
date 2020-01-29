# Linux

Edge Delta provides a convenient self extracting installer package supporting common Linux distributions such as Ubuntu, Debian, CentOS, RHEL.

## Download and installation

Contact Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to get a download link. Replace `download_link` below with the URL received from Edge Delta team and run following command in an empty folder.

```text
wget download_link -v
chmod +x edgedelta_*_linux_amd64.sh
sudo ./edgedelta_*_linux_amd64.sh
```

Script deploys Edge Delta into `path /opt/edgedelta/agent/` and system service `edgedelta` starts automatically with default configuration.

Check the service status using one of the following commands depending on your distribution.

```text
service edgedelta status
systemctl status edgedelta
/etc/init.d/edgedelta status
```

Configuration path is `/opt/edgedelta/agent/conf.yaml`

Log file path is `/opt/edgedelta/agent/edgedelta.log`

