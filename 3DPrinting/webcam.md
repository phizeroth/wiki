---
title: Webcam (OctoPrint)
description: Settings for webcam optimization with OctoPrint
published: true
date: 2023-03-24T02:19:20.085Z
tags: #3dp, octoprint
editor: markdown
dateCreated: 2022-10-07T16:35:30.068Z
---

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

## Change camera settings
```bash
ssh pi@octopi.local
sudo nano /boot/octopi.txt
```

Uncomment and edit the following line:
```
camera_usb_options="-r 640x480 -f 15"
```
`-r`: resolution
`-f`: framerate

## References
- https://community.octoprint.org/t/disable-autofocus-on-usb-webcam-config-using-v4l2-ctl-on-linux/30393
- https://iotrant.com/2020/02/25/properly-configuring-a-camera-in-octoprint/
- https://community.octoprint.org/t/available-mjpg-streamer-configuration-options/1106