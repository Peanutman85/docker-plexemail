![https://linuxserver.io](http://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)

The [LinuxServer.io](https://www.linuxserver.io/) team brings you another quality container release featuring auto-update on startup, easy user mapping and community support. Be sure to checkout our [forums](https://forum.linuxserver.io/index.php) or for real-time support our [IRC](https://www.linuxserver.io/index.php/irc/) on freenode at `#linuxserver.io`.

# linuxserver/plexemail

Is a script that aggregates all new TV and movie releases for the past x days then writes to your web directory and sends out an email.

## Usage

```
docker create --name=plexemail \
	-v /etc/localtime:/etc/localtime:ro \
	-v <path to config>:/config \
	-v <path to "Plex Media Server" folder>:/plex \
	-e PGID=<gid> \
	-e PUID=<uid>  \
	-p 80:8080 \
	linuxserver/plexemail
```

**Parameters**

* `-p 8080` - the port(s)
* `-v /etc/localtime` for timesync - *optional*
* `-v /config` - PlexEmail config folder
* `-v /plex` - "Plex Media Server" folder from Plex server
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on phusion-baseimage with ssh removed, for shell access whilst the container is running do `docker exec -it plexemail /bin/bash`.

### User / Group Identifiers

**TL;DR** - The `PGID` and `PUID` values set the user / group you'd like your container to 'run as' to the host OS. This can be a user you've created or even root (not recommended).

Part of what makes our containers work so well is by allowing you to specify your own `PUID` and `PGID`. This avoids nasty permissions errors with relation to data volumes (`-v` flags). When an application is installed on the host OS it is normally added to the common group called users, Docker apps due to the nature of the technology can't be added to this group. So we added this feature to let you easily choose when running your containers.

## Setting up the application 

* Edit the config.conf in the /config folder.
* Update the /cron/crontab as necessary.
* See project GIT for more information on configuration: https://github.com/jakewaldron/PlexEmail

## Updates

* Upgrade to the latest version simply `docker restart plexmail`.
* To monitor the logs of the container in realtime `docker logs -f plexmail`.



## Versions

+ **10.11.2015** Initial Release 
