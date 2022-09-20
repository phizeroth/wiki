---
title: Development Notes
description: 
published: true
date: 2022-09-20T19:08:04.869Z
tags: 
editor: markdown
dateCreated: 2022-02-14T15:57:50.712Z
---

## Archive and encrypt secrets

Always encrypt secrets folder before committing to git if any auth files have been changed.

```shell
tar -cvf auth.tar auth/
gpg -c auth.tar
```

## Missing library
If receiving an error about missing `libbrcmGLESv2.so` or `libbrcmEGL.so`, a symbolic link needs to be created the following files:

```shell
apt install libgles-dev libegl-dev
cd /usr/lib/arm-linux-gnueabihf/
sudo ln -s libGLESv2.so libbrcmGLESv2.so
sudo ln -s libEGL.so libbrcmEGL.so
```