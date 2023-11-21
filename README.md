# README

Basic Portainer setup from https://www.portainer.io/blog/replacing-docker-desktop-on-windows:

```console
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 \
  --name portainer --restart=always \
  -v /var/run/docdker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:2.11.0
```

After running the above, Portainer should be available at https://localhost:9443/

Instead of the above `docker run` command, on should be able to run the following Docker Compose file

```yaml
name: portainer_ce
services:
    portainer-ce:
        ports:
            - 8000:8000
            - 9443:9443
        container_name: portainer
        restart: always
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - portainer_data:/data
        image: portainer/portainer-ce:2.11.0
volumes:
    portainer_data:
        external:
            name: portainer_data
```

using

```console
docker-compose up -d
```

