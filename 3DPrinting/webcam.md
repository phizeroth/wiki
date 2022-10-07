---
title: Webcam
description: 
published: true
date: 2022-10-07T16:38:14.357Z
tags: #3dp
editor: markdown
dateCreated: 2022-10-07T16:35:30.068Z
---

# Webcam
## Disable autofocus

Autofocusing webcams may struggle with the constant movement of the bed. To manually disable autofocus:
```bash
ssh pi@octopi.local
sudo v4l2-ctl --set-ctrl=focus_auto=0
sudo v4l2-ctl --set-ctrl=focus_absolute=40
```

> Note: The "v4l2" includes the letter *l*, *not* the numeral *1*
{.is-info}


To re-enable autofocus:
```bash
sudo v4l2-ctl --set-ctrl=focus_auto=1
```

## References
- https://community.octoprint.org/t/disable-autofocus-on-usb-webcam-config-using-v4l2-ctl-on-linux/30393