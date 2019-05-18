---
title: Use Jupyter notebook remotely
layout: post
description: The farthest distance is between local and remote.
---

Let us see how to deal with it.

### Install `Jupyter`

The first thing you need to do is to install `Jupyter` in both local and remote:

```bash
$ pip install jupyter
```

### Start `Jupyter` in remote

Locate in the desired direcory in remote host, then type:

```bash
$ jupyter notebook --no-browser --port=8889
```

###Connect local and remote

In local, type below code:

```bash
$ ssh -N -f -L localhost:8888:localhost:8889 user@remote_host
```

Remember to modify `user` and `remote_host`.

### Open browser

The address is `localhost:8888`.