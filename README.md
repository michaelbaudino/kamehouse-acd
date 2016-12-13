# KameHouse Docker containers

## Torrents

Fetch and build required Docker images:
```
docker-compose -f torrents.yml pull && docker-compose -f torrents.yml build
```

Install Let's Encrypt certificates:
```
docker-compose -f torrents.yml run --service-ports nginx letsencrypt-install --domain <example.com> --email <root@example.com> [--staging]
```

Run:
```
docker-compose -f torrents.yml [-f torrents.production.yml] [-f torrents.override.yml] up [-d]
```

Renew Let's Encrypt certificates:
```
docker-compose -f torrents.yml exec nginx letsencrypt-renew [--staging] [--force-renewal]
```

Follow logs with:
```
docker-compose -f torrents.yml logs -f nginx
```

Open a shell in running container:
```
docker-compose -f torrents.yml exec nginx bash
```

### Provision on a Scaleway server using Docker Machine

0. Make sure you have the [Scaleway CLI](https://github.com/scaleway/scaleway-cli) tool authenticated
1. Create the server: `docker-machine create -d scaleway --scaleway-name=torrents torrents`
2. Use this server config: `docker-machine use torrents` or `eval "$(docker-machine env torrents)"`
3. Deploy the services using the instructions above
