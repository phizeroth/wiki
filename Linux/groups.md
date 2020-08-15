---
title: Linux groups
description: 
published: true
date: 2020-08-15T15:56:59.801Z
tags: linux
editor: markdown
---

## Using Linux groups

Create a new group:
```
groupadd mygroup
```

Add user to a group:
```
sudo usermod -aG mygroup myuser
```

List users in a group:
```
grep mygroup /etc/group
```

List groups that a user is a member of:
```
groups myuser
```

Check your current active group:
```
id -gn
```

Change your current active group:
```
newgrp mygroup
```

Change a folder's group permission:
```
chown myuser:mygroup myfolder
```

### Using `setgid`

Set a folder's `gid`, so that all files and subfolders created within that folder will inherit that group:
```
chmod g+s myfolder
```

A folder with a `gid` set will show an `s` in the last group permissions character:
`drwxr-sr-x   5 phi wiki  4096 Aug  6 18:34 data/`

Unset the `gid`:
```
chmod g-s myfolder
```

## References
- https://www.linux.com/topic/desktop/how-manage-users-groups-linux/
- https://linuxconfig.org/how-to-use-special-permissions-the-setuid-setgid-and-sticky-bits