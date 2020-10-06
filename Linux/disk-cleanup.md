---
title: disk cleanup
description: easy ways to tidy up some free disk space
published: true
date: 2020-10-06T20:44:19.317Z
tags: linux
editor: markdown
---

## Informational

### Folder sizes

Interactive directory of folders with folder sizes (See [Folder sizes](/Linux/utilities#folder-sizes)):
```shell-session
ncdu / -x
```

### Review installed apt packages
The simple apt way is with `apt list --installed`. However, this will not show disk usage for the packages. An estimation can be done with this lovely command:
```shell-session
dpkg-query -Wf '${db:Status-Status} ${Installed-Size}\t${Package}\n' | sed -ne 's/^installed //p'|sort -n
```

Alternatives:
- Install the [debian-goodies](https://packages.debian.org/stretch/debian-goodies) package and simply use the command `dpigs`. 
- Install the [wajig](https://wiki.debian.org/Wajig) package and use the command `wajig large`.

> None of these methods are able to show the _actual_ size, but rather the standard _installed_ size.{.is-info}

## Cleanup

### Remove unused apt dependencies and Linux kernels
```shell-session
sudo apt autoremove
```

### Clean up apt cache
View the size of apt cache:
```shell-session
sudo du -sh /var/cache/apt
```

Clean up outdated packages:
```shell-session
sudo apt autoclean
```

Delete apt cache completely:
```shell-session
sudo apt clean
```

### Clear system journal logs
Check log size:
```shell-session
journalctl --disk-usage
```

Clear logs past a certain age:
```shell-session
sudo journalctl --vacuum-time=3d
```

## References
- https://itsfoss.com/free-up-space-ubuntu-linux/
- https://unix.stackexchange.com/questions/40442/which-installed-software-packages-use-the-most-disk-space-on-debian