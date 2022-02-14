---
title: Development Notes
description: 
published: true
date: 2022-02-14T15:57:50.712Z
tags: 
editor: markdown
dateCreated: 2022-02-14T15:57:50.712Z
---

## Archive and encrypt secrets
```shell
tar -cvf keys.tar *.json
gpg -c keys.tar
```