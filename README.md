# KameHouse Docker containers

Fetch required Docker images:
```
docker-compose -f nginx.yml -f transmission.yml pull
```

Install Let's Encrypt certificates:
```
docker-compose -f nginx.yml run --service-ports nginx letsencrypt-install --domain <example.com> --email <root@example.com> [--staging]
```

Run:
```
docker-compose -f nginx.yml -f transmission.yml [-f transmission.production.yml] up [-d]
```

Renew Let's Encrypt certificates:
```
docker-compose -f nginx.yml exec nginx letsencrypt-renew [--staging] [--force-renewal]
```

Follow logs with:
```
docker-compose -f nginx.yml logs -f nginx
```

Open a shell in running container:
```
docker-compose -f nginx.yml exec nginx bash
```
