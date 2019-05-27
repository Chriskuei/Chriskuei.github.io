---
title: VS Code Remote Development
layout: post
description: VS Code is best in the world...
---

**Visual Studio Code Remote Development** is an amazing feature which allows you to use remote machine as a full-featured development environment. Once connected to a server, you can interact with files and folders anywhere on the remote filesystem.

### Intallation

- Install [Visual Studio Code Insiders](https://code.visualstudio.com/insiders/).
- Install Remote Development extension pack in your VS Code Insiders.

### Set up SSH key based authentication

- Check to see if you already have an SSH key. The locating address is at `~/.ssh/id_rsa_pub`. If not, then generate one:

```bash
$ ssh-keygen -t rsa -b 4096
```

- Add the contents of your local public key to the remote host:

```bash
$ ssh-copy-id your-user-name-on-host@host-fqdn-or-ip-goes-here
```

### Run Remote-SSH: Connect to Host

Press `Command+Shift+P`, choose **Remote-SSH**, then enter the host and your user on the host in the input box as follows: `user@hostname` . 

That's Done.

### Remember frequently connected host

Run **Remote-SSH: Open Configuration File...** and add the host to the file using the SSH config file format:

```basic
Host example-remote-linux-machine
    User your-user-name-here
    HostName host-fqdn-or-ip-goes-here

Host example-remote-linux-machine-with-identity-file
    User your-user-name-on-host
    HostName another-host-fqdn-or-ip-goes-here
    IdentityFile ~/.ssh/id_rsa-remote-ssh
```