# Synology-NextCloud
Setup NextCloud on Synology

0. Synology DSM 6.2 with following packages are installed
* Web Station
* Apache Server 2.2
* Maria DB 10
* PHP 5.6

1. Create share to store NextCloud data. Make sure allow read/write to `http` group
![share-permission](https://github.com/emelianov/Synology-NextCloud/blob/master/images/share-perm.png)
1. Login to Synology usin your favorit ssh client as *admin*

2. Switch to root. (Use *admin* password again)
```
admin@DSM6:/$ sudo -i
password:
```

3. Go to to web server folder
```
root@DSM6:~# cd /volume1/web/
root@DSM6:/volume1/web#
```

4. Go to [Install - NextCloud](https://nextcloud.com/install/#instructions-server), click `Detail download and options` and Copy Link to `tar.bz2` archive. (https://download.nextcloud.com/server/releases/nextcloud-12.0.2.tar.bz2 now)

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

8. Change ownship for NextCloud data directory
```
root@DSM6:/volume1/web# chown root:http /volume1/nextcloud
```

9. Restrict everyone access to NextCloud data
```
root@DSM6:/volume1/web# chmod 770 /volume1/nextcloud
```
That's all with CLI.

10. Set http back-server to Apache 2.2 and PHP to 5.6
![back-server](https://github.com/emelianov/Synology-NextCloud/blob/master/images/web-general.png)

11. Add `:/dev/urandom:/volume1/nextcloud` to end of open_basedir
![php-settings](https://github.com/emelianov/Synology-NextCloud/blob/master/images/web-php2.png)

12. Make sure that following Extensions are enabled
* culr
* gd
* openssl
* pdo_mysql
* zip

13. Reset Maria DB password to known. Also note port on whitch DB is listen for requests (3307 at screenshot).
![php-settings](https://github.com/emelianov/Synology-NextCloud/blob/master/images/db-port.png)

14. Open `<synology_ip>/nextcloud` in browser. Fill
* Username
* Password
* Path to NextCloud Share (created at step 1.)
* DB user (root)
* DB user password (set at step 13.)
* DB name
* Maria DB IP:PORT (from step 13.) It's better to specify IP (`127.0.0.1`) rather than name (`localhost`) as name may not work in same cases.
![nextcloud-start](https://github.com/emelianov/Synology-NextCloud/blob/master/images/nc-create.png)

15. Click `Finish` and wait while NextClout to be initialized
