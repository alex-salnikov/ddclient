# Setup "ddclient" for dynamic DNS-update in Cloudflare
1. in your [Clodflare dashboard](https://dash.cloudflare.com) - configure your DNS-zone (domain, sub-domain(s)) and [create API-token](https://developers.cloudflare.com/fundamentals/api/get-started/create-token/)
2. copy [docker-compose.yml](docker-compose.yml) and [ddclient.conf](./ddclient.conf) to your working-directory
3. in [ddclient.conf](./ddclient.conf) set your zone and domain/sub-domain (! A-record for sub-domain must already exist in your zone)
```
..
zone=your-zone.tld, \                       # <-- specify your zone-id
..
password='your_cloudflare_token',           # <-- specify your cloudflare token
your-zone.tld,sub-domain.your-zone.tld      # <-- specify your domain and/or sub-domain(s) to be updated
```
4. review configuration of [docker-compose.yml](./docker-compose.yml)
5. start container
```sh
docker compose up -d    # start container
docker compose ps       # check that container is running
docker logs ddclient    # check logs
```
6. Check logs by running: `docker logs ddclient`
```log
$ docker compose ps
NAME       IMAGE                                 COMMAND   SERVICE    CREATED          STATUS          PORTS
ddclient   lscr.io/linuxserver/ddclient:latest   "/init"   ddclient   11 seconds ago   Up 10 seconds

$ docker logs ddclient
[migrations] started
[migrations] no migrations found
───────────────────────────────────────

      ██╗     ███████╗██╗ ██████╗
      ██║     ██╔════╝██║██╔═══██╗
      ██║     ███████╗██║██║   ██║
      ██║     ╚════██║██║██║   ██║
      ███████╗███████║██║╚██████╔╝
      ╚══════╝╚══════╝╚═╝ ╚═════╝

   Brought to you by linuxserver.io
───────────────────────────────────────

To support LSIO projects visit:
https://www.linuxserver.io/donate/

───────────────────────────────────────
GID/UID
───────────────────────────────────────

User UID:    1000
User GID:    1000
───────────────────────────────────────

[custom-init] No custom files found, skipping...
Setting up watches.
Watches established.
[ls.io-init] done.
SUCCESS:  updating sub-domain.your-zone.tld: IPv4 address set to 12.34.56.78
```


# References
- https://github.com/linuxserver/docker-ddclient
- https://www.davidschlachter.com/misc/cloudflare-ddclient
- https://developers.cloudflare.com/fundamentals/api/get-started/create-token/
