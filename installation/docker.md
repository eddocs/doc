# Docker

Edge Delta Docker image can be run on hosts running Docker environment to ingest log data from other Docker containers.

## Docker registry access

To be able to run Edge Delta Docker image, running host needs to have Edge Delta Docker registry access.

Contact info@edgedelta.com to receive Docker registry username and password for your organization.

Replace your_username and your_password parts in command below and run on hosts where you will run Edge Delta Docker container.

```
docker login registry.gitlab.com -u your_username -p your_password
```

## Running the container

You may use a local configuration file or let Edge Delta container to fetch its configuration from the configuration backend.

### Run with local configuration file

Replace $PWD/config.yml with absolute path of the local configuration file on host.

```
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

### Run with configuration API token and configuration backend

Replace your_api_token part in command with the token you receive from info@edgedelta.com.

Container should have internet access to fetch the configuration.

```
docker run -it \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-e "ED_API_TOKEN=your_api_token" \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

## Resource limitations

You can limit the cpu or memory resources used by Edge Delta container as seen below.

```
docker run -it --cpus=".25" --memory="256m" \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v $PWD/config_docker.yml:/edgedelta/config.yml \
registry.gitlab.com/edgedelta/edgedelta/agent:latest
```

