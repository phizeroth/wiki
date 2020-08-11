---
title: Handy Linux utilities
description: 
published: true
date: 2020-08-11T16:46:05.986Z
tags: linux
editor: markdown
---



## Resource monitor
```
htop
```

![htop.png](/assets/htop.png)

Press <kbd>F6</kbd> to select a column to sort by.

## Folder sizes
```
ncdu /
```
![ncdu.png](/assets/ncdu.png)

For WSL, exclude your Windows system in the results with one of two ways:
```
ncdu / -x
```
```
ncdu / --exclude /mnt
```
