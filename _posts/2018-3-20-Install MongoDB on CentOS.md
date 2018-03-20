---
title: Install MongoDB on CentOS
layout: post
description: I do not have a root privilege...
---



### Install

#### Download the binary files


```bash
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.3.tgz
```

#### Extract

```
tar -zxvf mongodb-linux-x86_64-3.6.3.tgz
```

#### Create target directory

```bash
mkdir -p mongodb
cp -R -n mongodb-linux-x86_64-3.6.3/ mongodb
```

#### Modify shell's rc file

```bash
export PATH=<mongodb-install-directory>/bin:$PATH
eg. export PATH=~/mongodb/mongodb-linux-x86_64-3.6.3/bin:$PATH
```



### Run

#### Create the data directory

```bash
mkdir -p ~/mongodb/data/db
```

#### Run MongoDB

Specify the path of the data directory

```bash
mongod --dpath ~/mongodb/data/db
```

#### Verity

If success, the process will output for the following line:

```bash
[initandlisten] waiting for connections on port 27017
```

#### Begin using MongoDB

```bash
mongo --host 127.0.0.1:27017
```

