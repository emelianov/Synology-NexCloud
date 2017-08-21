# Synology-NexCloud
Setup NextCloud on Synology

0. Synology packages needs to be installed:
* Web Station
* Apache 2.2
* Maria DB

1. Login to Synology usin your favorit ssh client as *admin*
2. Switch to root. Use *admin* password again
```
admin@DSM6:/$ sudo -i
password:
```
3. Go to to web server folder
```
root@DSM6:~# cd /volume1/web/
root@DSM6:/volume1/web#
```
4. Go to [Install - NextCloud](https://nextcloud.com/install/#instructions-server) and Copy Link to `tar.bz2` archive. (https://download.nextcloud.com/server/releases/nextcloud-12.0.2.tar.bz2 now)
5. Download NextCloud package to local
```
root@DSM6:/volume1/web# wget https://download.nextcloud.com/server/releases/nextcloud-12.0.2.tar.bz2
--2017-08-21 20:21:34--  https://download.nextcloud.com/server/releases/nextcloud-12.0.2.tar.bz2
Resolving download.nextcloud.com... 88.198.160.133
Connecting to download.nextcloud.com|88.198.160.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 42756355 (41M) [application/x-bzip2]
Saving to: 'nextcloud-12.0.2.tar.bz2'

100%[=====================================================================================================>] 42,756,355  3.64MB/s   in 20s

2017-08-21 20:21:55 (1.99 MB/s) - 'nextcloud-12.0.2.tar.bz2' saved [42756355/42756355]

root@DSM6:/volume1/web#
```
6. Extract downloaded package
```
root@DSM6:/volume1/web# tar -xf nextcloud-12.0.2.tar.bz2
```
7. Change owner to `http`
```
root@DSM6:/volume1/web# chown -R http:http nextcloud
```
That's all with CLI.
