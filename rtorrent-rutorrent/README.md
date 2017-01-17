# RuTorrent Image


## Tag available
* latest [(rutorrent/latest/Dockerfile)](https://github.com/xataz/dockerfiles/blob/master/rutorrent/latest/Dockerfile)
* latest-filebot, filebot [(rutorrent/latest-filebot/Dockerfile)](https://github.com/xataz/dockerfiles/blob/master/rutorrent/latest-filebot/Dockerfile)

## Description
What is [RuTorrent](https://github.com/Novik/ruTorrent) ?

ruTorrent is a front-end for the popular Bittorrent client rtorrent.
This project is released under the GPLv3 license, for more details, take a look at the LICENSE.md file in the source.

What is [rtorrent](https://github.com/rakshasa/rtorrent/) ?

rtorrent is the popular Bittorrent client.


## BUILD IMAGE
### Build arguments
* BUILD_CORES : Number of cpu's core for compile (default : empty for use all cores)
* MEDIAINFO_VER : Mediainfo version (default : 0.7.82)
* RTORRENT_VER : rtorrent version (default : 0.9.6)
* LIBTORRENT_VER : libtorrent version (default : 0.13.6)
* WITH_FILEBOT : Choose if install filebot (default : no)
* FILEBOT_VER : filebot version (default : 4.7.2)

### simple build
```shell
docker build -t xataz/rtorrent-rutorrent github.com/xataz/dockerfiles.git#master:rtorrent-rutorrent
```

### Build with arguments
```shell
docker build -t xataz/rtorrent-rutorrent:custom --build-arg WITH_FILEBOT=YES --build-arg RTORRENT_VER=0.9.4 github.com/xataz/dockerfiles.git#master:rtorrent-rutorrent
```


## Configuration
### Environments
* UID : Choose uid for launch rtorrent (default : 991)
* GID : Choose gid for launch rtorrent (default : 991)
* WEBROOT : (default : /)

### Volumes
* /data : Folder for download torrents
* /home/torrent/settings : Folder for ruTorrent's settings if you need to load your own settings like cookies, ratios and such. Any files in here will be copied in `/nginx/www/html/<WEBROOT>/share/`

#### data Folder tree
* /data/.watch : Rtorrent watch directory
* /data/.session : Rtorrent save statement here
* /data/torrents : Rtorrent download torrent here
* /data/Media : If filebot version, rtorrent create a symlink
* /nginx/www/html/<WEBROOT>/share/ : rutorrent configuration

### Ports
* 8080


## Usage
### Simple launch
```shell
docker run -dt -p 8080:8080 xataz/rtorrent-rutorrent
```
URI access : http://XX.XX.XX.XX:8080

### Advanced launch
```shell
docker run -dt -p 80:8080 \
	  -v /docker/data:/data \
	  -e UID=1001 \
	  -e GID=1001 \
    -e WEBROOT=/rutorrent \
	xataz/rtorrent-rutorrent:filebot
```
URI access : http://XX.XX.XX.XX/rutorrent
