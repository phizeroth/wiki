---
title: disk cleanup
description: easy ways to tidy up some free disk space
published: true
date: 2020-10-06T17:19:54.541Z
tags: linux
editor: markdown
---

### Remove unused apt packages and Linux kernels
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
```
journalctl --disk-usage
```

Clear logs past a certain age:
```
sudo journalctl --vacuum-time=3d
```

### References
- https://itsfoss.com/free-up-space-ubuntu-linux/