# KameHouse Docker containers

Build:
```
docker-compose build
```

Install Let's Encrypt certificates:
```
docker-compose run -p 80:80 nginx letsencrypt-install --domain <example.com> --email <root@example.com> [--staging]
```

Run:
```
docker-compose up
```

Renew Let's Encrypt certificates:
```
docker-compose exec nginx letsencrypt-renew [--staging] [--force-renewal]
```

Follow logs with:
```
docker-compose logs -f nginx
```

Open a shell in running container:
```
docker-compose exec nginx bash
```
