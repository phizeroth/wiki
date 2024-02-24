---
title: ssh
description: 
published: true
date: 2024-02-24T20:28:00.290Z
tags: 
editor: markdown
dateCreated: 2023-07-27T22:37:49.197Z
---

## Create

```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_ed -C "user@host"
```

Optionally, add `-a #` option to specify number of KDF rounds for passphrase encryption (default is 16).
```bash
ssh-keygen -a 128 -t ed25519 -C "user@host"
```

## Managing multiple keys
Specify the key to use:
```bash
ssh -i ~/.ssh/id_ed "user@host"
```
https://www.redhat.com/sysadmin/manage-multiple-ssh-key-pairs