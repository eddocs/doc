# Linux

Edge Delta provides a convenient self extracting installer package supporting common Linux distributions such as Ubuntu, Debian, CentOS, RHEL.

## Download and installation

Edge Delta sales team will provide you the URL. Replace download_link with given URL and run following commands in an empty folder.

```
wget download_link -v
chmod +x edgedelta_*_linux_amd64.sh
sudo ./edgedelta_*_linux_amd64.sh
```

Script deploys Edge Delta into path /opt/edgedelta/agent/ and system service edgedelta starts automatically.

You may check the service status using one of the following commands depending on your distribution
```
service edgedelta status
systemctl status edgedelta
/etc/init.d/edgedelta status
```

Configuration path is /opt/edgedelta/agent/conf.yaml

Log file path is /opt/edgedelta/agent/conf.yaml
