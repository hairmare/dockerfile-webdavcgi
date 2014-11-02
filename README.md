# WebDAV CGI on Docker

This is for running [WebDAV CGI](http://webdavcgi.sourceforge.net/) on [docker](https://www.docker.com/).

Consider this experimental. There is still some work to do until all of this
has been upstreamed properly.

* [ ] get the [webdavcgi-1.0.0 ebuild](https://github.com/hairmare/gentoo-proxy-maintenance-webdavcgi/blob/master/www-apps/webdavcgi/webdavcgi-1.0.0.ebuild) into gentoo proper
* [ ] add packages needed to exploit all of the features from webdavcgi (soffice, mysql, whatever else floats my boat) as well as use flags in ebuild
* [ ] switch to an [official gentoo base image](https://github.com/gentoo/docker-brew-gentoo)

## Usage

Start up a webdavcgi instance on port 80

``
docker run -d -n webdavcgi hairmare/webdavcgi
``

Attach to the instance

``
sudo nsenter --target `docker inspect --format '{{.State.Pid}}' webdavcgi` --mount --uts --ipc --net --pid
``

Add users

``
useradd -m test
htpasswd -c /etc/webdavcgi-1.0/default/users.htpasswd test
``

Login at http://localhost.
