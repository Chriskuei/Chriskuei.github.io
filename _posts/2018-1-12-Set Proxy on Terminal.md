---
title: Set Proxy on Terminal
layout: post
description: Nothing can stop you.
---



#### Set Proxy

Add below to `.zshrc`

```bash
function setproxy() {
	export http_proxy=http://address:port
	export https_proxy=http://address:port
}
function unsetproxy() {
	# unset ALL_PROXY
	unset http_proxy
	unset https_proxy
}
alias sp="setproxy"
alias usp="unsetproxy"
alias ip="curl cip.cc"
```



#### Locale

Modify `.zshrc` or `.bashrc`

- zsh

```bash
LC_CTYPE=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

- bash

```bash
export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```