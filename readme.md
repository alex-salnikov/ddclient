# Setup ddclient for dynamic DNS-update
1. configure your zone and domain/sub-domain in [ddclient.conf](./ddclient.conf)
2. review configuration of [docker-compose.yml](./docker-compose.yml)
3. start container
```sh
docker compose up -d    # start container
docker compose ps       # check running container
docker logs ddclient    # check logs
```


# References
- https://github.com/linuxserver/docker-ddclient
- https://www.davidschlachter.com/misc/cloudflare-ddclient
