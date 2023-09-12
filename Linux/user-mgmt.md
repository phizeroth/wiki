---
title: user management
description: 
published: true
date: 2023-09-12T16:29:21.415Z
tags: linux
editor: markdown
dateCreated: 2023-09-12T16:26:56.965Z
---

# User Management

## New user

Use `-m` tag to automatically set up home directory for new user.
```shell
useradd -m username
```
If you forgot to add `-m` flag on user creation, it can be easily added in afterwards

```shell
mkhomedir_helper username
```

### Add user to sudo group
```shell
usermod -aG sudo username
```