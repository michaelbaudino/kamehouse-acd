# KameHouse Docker containers

## Nginx

This is the base image meant to be used by the other ones. It includes:

* `nginx` with HTTPS forced
* `letsencrypt`

Build with:
```shell
docker build nginx -t kamehouse/nginx
```

Setup with:
```shell
docker run -it --net=host -v letsencrypt:/etc/letsencrypt/ -e "DOMAIN_NAME=example.com" -e "ADMIN_EMAIL=root@example.com" kamehouse/nginx setup
```

Start with:
```shell
docker run -d --net=host -v letsencrypt:/etc/letsencrypt/ --name kamehouse-nginx kamehouse/nginx
```

Follow logs with:
```shell
docker logs -f kamehouse-nginx
```

Update certs with (can be added to `crontab`):
```shell
docker exec -it kamehouse-nginx renew-letsencrypt-certs
```

## Torrents

This is image in charge of downloading media files. It is derived from the Nginx base image and includes:

* `transmission-daemon`
* `flexget`

Build with:
```shell
docker build torrents -t kamehouse/torrents
```

Setup with:
```shell
docker run -it --net=host -v letsencrypt:/etc/letsencrypt/ -e "DOMAIN_NAME=example.com" -e "ADMIN_EMAIL=root@example.com" kamehouse/torrents setup
```

Start with:
```shell
docker run -d --net=host -v letsencrypt:/etc/letsencrypt/ --name kamehouse-torents kamehouse/torrents
```
