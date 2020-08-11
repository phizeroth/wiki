---
title: Handy Linux utilities
description: 
published: true
date: 2020-08-11T15:29:45.368Z
tags: linux
editor: markdown
---



### Resource monitor
```
htop
```

![htop.png](/assets/htop.png)

Press <kbd>F6</kbd> to select a column to sort by.
</br>

### Folder sizes
```
ncdu /
```
![ncdu.png](/assets/ncdu.png)

For WSL, exclude the `/mnt` directory to exclude your Windows system in the results:
```
ncdu / --exclude /mnt
```
