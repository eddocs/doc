# Docker

Edge Delta Docker image can be run on hosts running Docker environment to ingest log data from other Docker containers.



## Docker Registry Access

To be able to run Edge Delta Docker image, running host needs to have Edge Delta Docker registry access.

Contact [info@edgedelta.com](mailto:info@edgedelta.com) to receive Docker registry username and password for your organization.

Replace your\_username and your\_password parts in command below and run on hosts where you will run Edge Delta Docker container.

```text
docker login registry.gitlab.com -u your_username -p your_password
```



## Running the Container

You may use a local configuration file or let Edge Delta container to fetch its configuration from the configuration backend.

### Run with Local Configuration File

Replace `$PWD/config.yml`with absolute path of the local configuration file on host.

```text
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

### Run with Configuration API Token and Configuration Backend

Replace `your_api_token` with the token you receive from [info@edgedelta.com](mailto:info@edgedelta.com) 

Container should have internet access to fetch the configuration.

```text
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-e "ED_API_TOKEN=your_api_token" \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

## Resource Limitations

You can limit the CPU or memory resources that Edge Delta container uses. In example below we are limiting Edge Delta container to utilize maximum 25% CPU and 256 MB of memory 

```text
docker run -it --cpus=".25" --memory="256m" \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config_docker.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

