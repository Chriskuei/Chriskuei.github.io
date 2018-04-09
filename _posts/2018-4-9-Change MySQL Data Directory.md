---
title: Change MySQL Data Directory
layout: post
description: It is MySQL…
---

#### Stop MySQL

```shell
sudo systemctl stop mysqld
```

#### Backup Data Directory

```shell
sudo cp -arp /var/lib/mysql /var/lib/mysql-old
```

#### Copy Data to New Location

```shell
sudo cp -arp /var/lib/mysql /data
```

#### Remove Original Data

```shell
sudo rm -rf /var/lib/mysql/*
```

#### Edit `/etc/fstab` File

```shell
echo "/data/mysql /var/lib/mysql none bind 0 0" >> /etc/fstab
```

#### Mount

```shell
sudo mount -a
```

#### Restart MySQL

```shell
sudo systemctl start mysqld
```

