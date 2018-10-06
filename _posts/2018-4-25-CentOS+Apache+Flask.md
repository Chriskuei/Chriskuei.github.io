---
title: CentOS+Apache+Flask
layout: post
description: Thank you for visit my website
---

### Install WSGI

Download from [GitHub](https://github.com/GrahamDumpleton/mod_wsgi/releases), compile from source:

```bash
$ ./configure --with-python=*your_python_path*
$ make
$ make install
```

Or install by pip

```bash
$ pip install mod_wsgi
```

You can find package path by `python -m site` , then copy mod_wsgi to Apache's modules directory

```bash
$ cp mod_wsgi.so /etc/httpd/modules/mod_wsgi.so
```



### Configure Apache

Open configure file

```bash
$ vim /etc/httpd/conf/httpd.conf
```

In configure file, add code:

```bash
WSGIScriptAlias /url /var/www/html/flask/flask.wsgi
WSGIScriptReloading On
<Directory "/var/www/html/flask">
	AllowOverride All
	Require all granted
</Directory>
```



### Configure WSGI

The directory structure is

```bash
flask/
├──app
|  ├── __init__.py
|  └── other.file
└── flask.wsgi
```

Edit `flask.wsgi`

```bash
import sys
import os

sys.path.insert(0, "/var/www/html/flask")
from app import app
application = app
```

Congratulation! All have done



### Questions

#### libpython3.6m.so.1.0

Apache log is store in `/etc/httpd/logs/error.log`. If this error occurs

> ```
> python3: error while loading shared libraries: libpython3.6m.so.1.0: cannot open shared object file: No such file or directory
> ```

Find `libpython3.6m.so.1.0` path

```bash
$ find / -name 'libpython3.6m.so.1.0'
```

Create `python3.conf` In directory `/etc/ld.so.conf.d`. Edit `python3.conf`

```bash
/usr/local/lib/ # This directory is where libpython3.6m.so.1.0 in
```

Then run

```bash
$ ldconfig
```

#### Fix "FAILED TO MAP SEGMENT FROM SHARED OBJECT: PERMISSION DENIED" 

We can temporarily turn off SElinux by making it in permissive mode

```bash
$ getenforce
Enforcing
$ sudo setenforce 0
$ getenforce
Permissive
```

If you want to permanently solve the problem, need to edit the selinux config file

```bash
$ sudo vim /etc/selinux/config
```

Change `SELINUX=enforcing` to `SELINUX=disabled`.