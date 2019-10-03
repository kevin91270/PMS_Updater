PMS_Updater Instructions by luluhoc
===========

This is updated version of PMS_Updater. Updater is confirmed to work on latest FreeNas 11.2-U6


If you have plex plugin installed [*Run First Five commands only first time, after that you need to run only the last command*]
```
pkg install ca_root_nss 
pkg install wget
pkg install perl5
fetch -o PMS_Updater.sh https://raw.githubusercontent.com/luluhoc/PMS_Updater/master/PMS_Updater.sh
chmod 755 PMS_Updater.sh
./PMS_Updater.sh -u [username] -p [password] -a -v
```
If after update you've got an error `Server settings are unavailable`
```
cd /usr/local/share/plexmediaserver/lib/
mv * ..
```
Restart Jail after and it should start working normally

If You have installed PLEX Pass Plugin [*Run First Five commands only first time, after that you need to run only the last command*]
```
pkg install ca_root_nss
pkg install wget
pkg install perl5
fetch -o PMS_Updater.sh https://raw.githubusercontent.com/luluhoc/PMS_Updater/master/PMS_UpdaterPLEXPASS.sh
chmod 755 PMS_Updater.sh
./PMS_Updater.sh -u [username] -p [password] -a -v
```

PMS_Updater.sh is a shell script for updating the Plex Media Server inside the FreeNAS Plex plugin


---

<a href="http://www.freenas.org/">FreeNAS</a> is an excellent open-source network attached storage project based on FreeBSD that is very capable of storing even the largest media libraries

<a href="http://plex.tv">Plex</a> is an amazing media server/client platform that can organize and stream those same media libraries.

FreeNAS has a plug-in architecture that makes running Plex Media Server on FreeNAS trivialy easy.  But the available Plex Media Server plug-in is only as recent as the latest publicly available release.

To address this I have made a script that can be copied into a running Plex Media Server plug-in, and without needing anything else installed it can search the Plex.tv download site using paid PlexPass credentials and check for newer versions.  If a newer version is found it can either be downloaded and held for admin approval or automatically installed to the server.

To use run PMS_Updater.sh as root. The following options can be used:

```
OPTIONS:
   -u      PlexPass username
             If -u is specified without -p then the script will
             prompt the user to enter the password when needed
   -p      PlexPass password
   -c      PlexPass user/password file
             When wget is run with username and password on the
             command line, that information is displayed in the
             process list for all to see.  A more secure method
             is to create a file readable only by root that is
             formatted like this:
               user={Your Username Here}
               password={Your Password Here}
   -l      Local file to install instead of latest from Plex.tv
   -d      download folder (default /tmp) Ignored if -l is used
   -a      Auto Update to newer version
   -f      Force Update even if version is not newer
   -r      Remove update packages older than current version
             Done before any update actions are taken.
   -v      Verbose
```
   
Running without the username/password or bad username/password will retrieve the latest public release rather than the latest Plex Pass release.

The script can also be called from a cronjob to check for updates on a regular schedule.
