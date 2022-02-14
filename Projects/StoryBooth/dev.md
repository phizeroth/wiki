---
title: Development Notes
description: 
published: true
date: 2022-02-14T17:23:26.668Z
tags: 
editor: markdown
dateCreated: 2022-02-14T15:57:50.712Z
---

## Archive and encrypt secrets
```shell
tar -cvf auth.tar auth/
gpg -c auth.tar
```