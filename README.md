# KameHouse Docker containers

## Torrents

Fetch required Docker images:
```
docker-compose -f transmission.yml pull
```

Install Let's Encrypt certificates:
```
docker-compose -f transmission.yml run --service-ports nginx letsencrypt-install --domain <example.com> --email <root@example.com> [--staging]
```

Run:
```
docker-compose -f transmission.yml [-f transmission.production.yml] [-f transmission.override.yml] up [-d]
```

Renew Let's Encrypt certificates:
```
docker-compose -f transmission.yml exec nginx letsencrypt-renew [--staging] [--force-renewal]
```

Follow logs with:
```
docker-compose -f transmission.yml logs -f nginx
```

Open a shell in running container:
```
docker-compose -f transmission.yml exec nginx bash
```
