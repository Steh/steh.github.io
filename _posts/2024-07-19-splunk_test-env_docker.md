---
title: "Using Splunk in Docker as a Test Environment: A Quick Guide"
categories: 
- informationsecurity
tags:
- blue team
- splunk
classes: 
- wide
excerpt: "Set up and manage a Splunk test environment using Docker, including app installation."
toc: true
---

## Start Basic Splunk Enterprise Environment

```bash
# most basic splunk environemnt
docker run -d -p 8000:8000 -e SPLUNK_START_ARGS='--accept-license' -e SPLUNK_PASSWORD='<password>' splunk/splunk:latest
```

Some Docker Basics

```bash
# get example commands
docker run -it splunk/splunk help

# list all running containers
docker ps

# stop a container
docker container stop <container_id>

# start a container
docker container start <container_id>

# enter container
docker exec -it <container_id> bash
```

## App installation

1. **Install from Splunkbase in GUI**
2. **Install from filesystem**

    ```bash 
    # copy app into container
    docker cp myapp.tar.gz splunk:/opt/splunk/etc/apps/
    
    # install the app
    docker exec -it splunk /opt/splunk/bin/splunk install app /opt/splunk/etc/apps/myapp.tar.gz -auth admin:your-password
    ```

3. **Install on Docker Start**

    ```bash
    # on startup
    docker run -d -p 8000:8000 -e SPLUNK_START_ARGS='--accept-license' \
        -e SPLUNK_PASSWORD='<password>' \
        -e SPLUNK_APPS_URL='https://splunkbase.splunk.com/app/2890/release/4.1.0/download' \
        -e SPLUNKBASE_USERNAME='<sb-username>' \
        -e SPLUNKBASE_PASSWORD='<sb-password>' \
        splunk/splunk:latest
    ```

## references

- [splunk.com Deploy and run Splunk Enterprise inside a Docker container][def]
- [splunk Docker-Splunk documentation!][def1]
- [docker.com splunk/splunk][def2]

[def]: https://docs.splunk.com/Documentation/Splunk/9.2.2/Installation/DeployandrunSplunkEnterpriseinsideDockercontainers
[def1]: https://splunk.github.io/docker-splunk/
[def2]: https://hub.docker.com/r/splunk/splunk/
