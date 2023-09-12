---
title: user management
description: 
published: true
date: 2023-09-12T16:26:56.965Z
tags: linux
editor: markdown
dateCreated: 2023-09-12T16:26:56.965Z
---

# User Management

## New user

Use `-m` tag to automatically set up home directory for new user.
```shell
useradd -m <user>
```

Add user to sudo group
```shell
usermod -aG sudo <user>
```