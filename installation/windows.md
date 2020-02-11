# Windows

Edge Delta has a very simple MSI installation, once complete, agent will run as a background service in Windows operating systems.

Edge Delta supports both 64 bit and 32 bit Windows platforms and a variety of operating system versions.

## Download

Contact Edge Delta team [info@edgedelta.com](mailto:info@edgedelta.com) to get a download link and your API key.

## UI Installation

After downloading the package, simply double click and follow the wizard.

You can change the installation directory where the Edge Delta agent will install during installation wizard, default path is "Program Files" or "Program Files \(x86\)" depending of your chosen platform.

Enter your API key when wizard prompts and finish installation.

# Command Line Silent Installation

After downloading the package start cmd.exe as Administrator. Change directory into download directory. Replace Api key you receive with YOUR_APIKEY and run following command:
```
start /wait msiexec /qn /i edgedelta-version_64bit.msi APIKEY="<YOUR_APIKEY>"
```

It will not output anything due to silent mode.

# Configuration

Once installation completed, the configuration file \(config.yaml\) and the agent log file \(edgedelta.log\) can be found in the installation directory.

{% hint style="info" %}
Edge Delta monitors section in the configuration file needs to be updated after installation.
{% endhint %}

## Troubleshooting

After installation Windows services UI \(services.msc\) and edgedelta.log file can be used to troubleshooting and to check the status of the agent.
