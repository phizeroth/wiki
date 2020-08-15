---
title: chmod
description: 
published: true
date: 2020-08-15T16:11:33.366Z
tags: linux
editor: markdown
---




<img src="/assets/classes.png.webp" style="filter: invert(.8)" />

File type may be `d` for directory or `-` for file.
An `s` permission in the group permission class of a directory indicates that new files in that folder will explicitly inherit its group permissions. See [using setgid](/Linux/groups#using-setgid).

  
  ||||||
|-|-|-|-|-|
**0**|-|-|-|no permissions
**1**|-|-|x|execute only
**2**|-|w|-|write only
**3**|-|w|x|write and execute
**4**|r|-|-|read only
**5**|r|-|x|read and execute
**6**|r|w|-|read and write
**7**|r|w|x|full control
