# Docker

Edge Delta has a Docker container image that can be deployed in a sidecar pattern to ingest log data from other Docker containers and provide isolation and encapsulation.



## Docker Registry Access

To be able to run Edge Delta Docker container image, running host needs to have Edge Delta Docker registry access.

Contact [info@edgedelta.com](mailto:info@edgedelta.com) to receive Docker registry username and password for your organization.

Replace `your_username` and `your_password` in command below and run on hosts where you will run Edge Delta Docker container.

```text
docker login registry.gitlab.com -u your_username -p your_password
```

## Running the Container

When it is time to run the Edge Delta container, you can either use a local configuration file or have the Edge Delta container fetch its configuration from the Edge Delta Central Configuration Backend \(CCB\).

### Run with a Local Configuration File

Replace `$PWD/config.yml`with absolute path of the local configuration file on host.

```text
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

### Run with an API Token Utilizing Central Configuration Backend \(CCB\)

Replace `your_api_token` with the token you receive from [info@edgedelta.com](mailto:info@edgedelta.com) 

Container must have internet access to fetch the configuration.

{% hint style="info" %}
More information about [CCB](../configuration-1/ccb.md) can be found under [Configuration](../configuration-1/) section
{% endhint %}

```text
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-e "ED_API_TOKEN=your_api_token" \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

## Limiting Resource Consumption

You can limit the CPU or memory resources that Edge Delta container consumes. In example below we are limiting Edge Delta container to utilize maximum 25% CPU and 256 MB of memory. 

```text
docker run -it --cpus=".25" --memory="256m" \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config_docker.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

