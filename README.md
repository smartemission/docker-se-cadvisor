# docker-se-cadvisor

Docker image for Google CAdvisor with local SE-patches

See https://github.com/google/cadvisor

> cAdvisor (Container Advisor) provides container users an understanding of the resource usage and performance characteristics of their 
> running containers. It is a running daemon that collects, aggregates, processes, and exports information about running containers. 
> Specifically, for each container it keeps resource isolation parameters, 
> historical resource usage, histograms of complete historical resource usage and network statistics. 
> This data is exported by container and machine-wide.

## Why SE Custom Docker Image

Need a custom Docker Image because of issue:
https://github.com/google/cadvisor/issues/1802
Once that is resolved we can use the official google/cadvisor `.

## Hosting

The SE Docker image is hosted as:
 [smartemission/se-cadvisor at DockerHub](https://hub.docker.com/r/smartemission/se-cadvisor).

Hosting for the parent Docker image `google/cadvisor`:

* Docker Image: https://hub.docker.com/r/google/cadvisor/
* Source code is maintained at https://github.com/google/cadvisor.

## Environment

At the moment no environment variables are required. As `CAdvisor` needs access to Docker resources
on the host, it requires volume mapping, at least within a `docker-compose` setup:


```
  cadvisor:
     # image: google/cadvisor
     image: smartemission/se-cadvisor:v0.28.3
     volumes:
       - /:/rootfs:ro
       - /var/run:/var/run:rw
       - /sys:/sys:ro
       - /var/lib/docker/:/var/lib/docker:ro
```

## Architecture

See https://github.com/google/cadvisor/tree/master/docs.

## Links

* SE Platform doc: http://smartplatform.readthedocs.io/en/latest/
* CAdvisor Docs: https://github.com/google/cadvisor/tree/master/docs