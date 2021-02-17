# How to install liferay 7 on debiann 10


## Pre-Checks


1. Check debian version that be true.
```shell
lsb_release -a

```
2. Check DNS settings

    It is better if you use the [Shecan](https://shecan.ir/) DNS servers.

> Edit below and add new name servers here and comment out existing name servers:

```shell
 nano /etc/resolve.conf
```

3. Update the system

```
apt-get update
apt update
apt upgrade
```

4. Install some utility packages:
```shell
apt install screen wget git unzip  -y

```

## Install database : Postgresql
* We install default `postgresql-11` version on Debian 10.

```bash
root@deb-liferay:~# apt install postgresql -y
```

> Enable the service

```bash
root@deb-liferay:~# systemctl enable postgresql
Synchronizing state of postgresql.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable postgresql
```
> Check the service
```shell
root@deb-liferay:~# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Wed 2021-02-17 12:35:34 +0330; 1h 49min ago
 Main PID: 3116 (code=exited, status=0/SUCCESS)

Feb 17 12:29:48 deb-liferay systemd[1]: Starting PostgreSQL RDBMS...
Feb 17 12:29:48 deb-liferay systemd[1]: Started PostgreSQL RDBMS.
Feb 17 12:35:34 deb-liferay systemd[1]: postgresql.service: Succeeded.
Feb 17 12:35:34 deb-liferay systemd[1]: Stopped PostgreSQL RDBMS.
```
> Change the data directory

```shell
root@deb-liferay:~# mkdir -p /home/data/postgres
root@deb-liferay:~# cp -Rf /var/lib/postgresql/11/main /home/data/postgres/
root@deb-liferay:~# chown -Rf postgres:postgres /home/data/postgres
root@deb-liferay:~# chmod 0700 /home/data/postgres
```
- Edit configuration file and change default `data_directory` by adding bellow line at end of file after `# Add settings for extensions here` line like

```shell
#------------------------------------------------------------------------------
# CUSTOMIZED OPTIONS
#------------------------------------------------------------------------------

# Add settings for extensions here
data_directory = '/home/data/postgres'
```

* Then restart the `postgresql` service

```shell
root@deb-liferay:~# systemctl restart postgresql.service
```
