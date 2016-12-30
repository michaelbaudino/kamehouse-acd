# Roadmap

## Task list

* [x] Configure `media` for [Emby](https://emby.media/)
* [x] Share `derrick` drives with `media`
* [x] Create `transmission` Docker image
* [x] Create `flexget` Docker image
  * [x] Configure ShowRSS integration
  * [x] Configure [clean_transmission plugin](http://www.flexget.com/Plugins/clean_transmission)
  * [ ] Configure [T411 plugin](http://www.flexget.com/Plugins/t411)
  * [ ] Configure [Betaseries plugin](http://www.flexget.com/Plugins/betaseries_list)
* [x] Configure `media` as a Docker Compose service based on [manual install procedure](https://gist.github.com/michaelbaudino/2b33ddaa061fb8fc6deb) (commands can be executed on host using `docker-machine ssh emby <command>`)

### Media file hierarchy

* [x] Mount [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) in `/mnt/.acd-fuse`
* [-] Mount local drive as `/mnt/.acd-cache`
* [x] Configure [encfs](https://github.com/vgough/encfs) to encrypt `/mnt/.acd-fuse` in `/mnt/acd-fuse`
* [x] Configure [encfs](https://github.com/vgough/encfs) to encrypt `/mnt/.acd-cache` in `/mnt/acd-cache`
* [x] Configure [unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) to merge `/mnt/acd-fuse` and `/mnt/acd-cache` in `/mnt/acd`
* [x] Configure removal of old files from cache
* [ ] Configure upload from cache to ACD

### Migration from Derrick

* [ ] Mount `/mnt/acd` from `media` into `/data/acd` on `derrick`
* [ ] Configure [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README) to merge `/data/acd` and `/data/public` in `/data/merged` on `derrick`
* [ ] Change symlinks in `/var/www/kamehouse/public/data` to point to `/data/merged` on `derrick`
* [ ] Move all content from `/data/public` to `/data/acd` on `derrick` (it should not change what `/data/merged` sees)

### Derrick unprovision

* [ ] Tell existing users to migrate to `media`
* [ ] Use `media` as default frontend
* [ ] Unprovision `derrick` :cry:

### Improvements

* [ ] Use `container_name` on some services to prevent scaling
* [ ] Configure hosts firewalls :question:
* [ ] Configure backup of `emby` users :question:
* [ ] Configure [CouchPotato](https://couchpota.to)
* [ ] Use [Sickrage](https://sickrage.github.io) or [Sonarr](https://github.com/Sonarr/Sonarr) instead of Transmission+Flexget+ShowRSS :question:

## Notes

### Target filesystem architecture

```
( ACD )═══ acd_cli ═══[ /mnt/.acd-fuse  ]═══ encfs ═══[ /mnt/acd-fuse  ]═══╗
                                                                           ╠═══ mhddfs ═══[ /mnt/acd ]
( DSSD )══════════════[ /mnt/.acd-cache ]═══ encfs ═══[ /mnt/acd-cache ]═══╝
```

### Target Derrick transition filesystem architecture:

```
[ /data/public ]═════════════════════════════════════════════════╗
                                                                 ╠═══ mhddfs ═══[ /data/merged ]
[ ACD ]═══ acd_cli ═══[ /data/.acd ]═══ encfs ═══[ /data/acd ]═══╝
```

### Literature

* https://github.com/yadayada/acd_cli
* https://github.com/vgough/encfs/
* https://github.com/rpodgorny/unionfs-fuse
* https://amc.ovh
