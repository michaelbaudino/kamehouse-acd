# Roadmap

* [x] Configure `media` for [Emby](https://emby.media/)
* [x] Share `derrick` drives with `media`
* [x] Create `transmission` Docker image
* [x] Create `flexget` Docker image
  * [x] Configure ShowRSS integration
  * [x] Configure [clean_transmission plugin](http://www.flexget.com/Plugins/clean_transmission)
  * [ ] Configure [T411 plugin](http://www.flexget.com/Plugins/t411)
  * [ ] Configure [Betaseries plugin](http://www.flexget.com/Plugins/betaseries_list)
* [ ] Configure `media` as a Docker Compose service based on [manual install procedure](https://gist.github.com/michaelbaudino/2b33ddaa061fb8fc6deb) (commands can be executed on host using `docker-machine ssh emby <command>`)

* [ ] Mount [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) in `/mnt/raw_acd` on `media`
* [ ] Mount [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) in `/mnt/raw_acd` on `torrents`
* [ ] Mount [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) in `/mnt/raw_acd` on `derrick`
* [ ] Configure [encfs](https://github.com/vgough/encfs) to encrypt `/mnt/raw_acd` in `/mnt/enc_acd` on `media`
* [ ] Configure [encfs](https://github.com/vgough/encfs) to encrypt `/mnt/raw_acd` in `/mnt/enc_acd` on `torrents`
* [ ] Configure [encfs](https://github.com/vgough/encfs) to encrypt `/mnt/raw_acd` in `/mnt/enc_acd` on `derrick`
* [ ] Configure [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README) or [unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) to merge `/mnt/enc_acd` and `/data/public` in `/cloud` on `media`
* [ ] Configure [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README) or [unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) to merge `/mnt/enc_acd` and `/data/public` in `/cloud` on `torrents`
* [ ] Configure [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README) or [unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) to merge `/mnt/enc_acd` and `/data/public` in `/cloud` on `derrick`

* [ ] Share `torrents` incoming directory with `media` for auto-organization
* [ ] Move all content from `derrick` drives to ACD
* [ ] Unprovision all `mhddfs` drives and use ACD everywhere (on `derrick` and `media`)
* [ ] Tell existing users to migrate to `media`
* [ ] Use `media` as default frontend
* [ ] Unprovision `derrick` :cry:

* [ ] Configure hosts firewalls :question:
* [ ] Configure backup of `emby` users :question:
* [ ] Configure [CouchPotato](https://couchpota.to)
* [ ] Use [Sickrage](https://sickrage.github.io/) instead of Transmission+Flexget+ShowRSS :question:

Target filesystem architecture:
```
[ Derrick ]═══sshfs═══[ /data/public ]════════════════════════════════╗
                                                                      ╠═══mhddfs|unionfs-fuse═══[ /storage/kamehouse ]
[ ACD ]═══acd_cli═══[ /storage/acd ]═══encfs═══[ /storage/acd_enc ]═══╝
```
