---
title: Install Zsh on CentOS
layout: post
description: Zsh, the most powerful shell in the universe.
---

### Install Zsh

#### Download Zsh


```bash
# Download
wget -O zsh.tar.gz https://sourceforge.net/projects/zsh/files/latest/download

mkdir zsh && tar -xvzf zsh.tar.gz -C zsh --strip-components 1
cd zsh
```

#### Compile Zsh

```bash
./configure --prefix=$HOME
make
make install
```



### Install Oh My Zsh

```bash
git clone --depth=1 https://github.com/robbyrussell/oh-my-zsh.git $HOME/.oh-my-zsh
cp $HOME/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```



### Login Zsh

#### Update ~/.bashrc

```bash
exec $HOME/bin/zsh
export PATH="$HOME/bin/zsh"
```

