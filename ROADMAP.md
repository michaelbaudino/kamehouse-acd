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
* [ ] Configure backup of `emby` users :question:
* [ ] Share `torrents` incoming directory with `media` for auto-organization
* [x] Configure [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) on `media`
* [ ] Configure [Amazon Cloud Drive](https://github.com/yadayada/acd_cli) on `derrick`
* [ ] Configure filesystem merging ACD and local drives on `derrick` using [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README)
* [ ] Configure filesystem merging ACD and `derrick` drives on `media` using [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README)
* [ ] Move all content from `derrick` drives to ACD
* [ ] Unprovision all `mhddfs` drives and use ACD everywhere (on `derrick` and `media`)
* [ ] Tell existing users to migrate to `media`
* [ ] Use `media` as default frontend
* [ ] Unprovision `derrick` :cry:
* [ ] Configure hosts firewalls :question:
* [ ] Configure [CouchPotato](https://couchpota.to)
* [ ] Use [Sickrage](https://sickrage.github.io/) instead of Transmission+Flexget+ShowRSS :question:
