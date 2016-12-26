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

### Provision on a Scaleway server using Docker Machine

0. Make sure you have the [Scaleway CLI](https://github.com/scaleway/scaleway-cli) tool authenticated
1. Create the server: `docker-machine create -d scaleway --scaleway-name=torrents torrents`
2. Use this server config: `docker-machine use torrents` or `eval "$(docker-machine env torrents)"`
3. Deploy the services using the instructions above


## Media

Fetch and build required Docker images:
```
docker-compose -f media.yml pull && docker-compose -f media.yml build
```

Install Let's Encrypt certificates:
```
docker-compose -f media.yml run --service-ports nginx letsencrypt-install --domain <example.com> --email <root@example.com> [--staging]
```

Setup Amazon Cloud Drive:
```
docker-compose -f media.yml run storage acd_auth
```

Generate an EncFS password and set it as `ENCFS_PASSWORD` in `.env` file:
```
dd bs=1 count=256 if=/dev/urandom status=none | base64 - | tr -d '\n' | echo "ENCFS_PASSWORD=$(</dev/stdin)" >> .env
```

> :warning: Backup this password very carefully: if lost, all your data will be permanently unrecoverable

Run:
```
docker-compose -fmedia{,.production}.yml up [-d]
```

### Provision on a Scaleway server using Docker Machine

0. Make sure you have the [Scaleway CLI](https://github.com/scaleway/scaleway-cli) tool authenticated
1. Create the server: `docker-machine create -d scaleway [--scaleway-commercial-type C2L] --scaleway-name=media media`
2. Eventually mount the DSSD volume: `docker-machine ssh media 'echo "/dev/sda1 /emby ext4 defaults 0 0" >> /etc/fstab'`
3. Configure Docker engine to allow shared propagation of volumes: `docker-machine ssh media 'mkdir -p /etc/systemd/system/docker.service.d/ && echo -e "[Service]\nMountFlags=shared" > /etc/systemd/system/docker.service.d/clear_mount_propagtion_flags.conf && systemctl daemon-reload && systemctl restart docker'`
4. Deploy the services using the instructions above
