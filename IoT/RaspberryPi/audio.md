---
title: audio
description: 
published: true
date: 2021-11-11T22:00:54.486Z
tags: 
editor: markdown
dateCreated: 2021-11-11T22:00:54.486Z
---

### arecord
Use `arecord` to work with audio capture devices.

To identify audio devices with their hardware address (card, subdevice):
```bash
arecord -l
```

### lsusb
If using a USB device, use `lsusb` to list all attached USB devices.