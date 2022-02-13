---
title: Software Setup
description: 
published: true
date: 2022-02-13T20:56:33.443Z
tags: 
editor: markdown
dateCreated: 2022-02-11T20:40:47.468Z
---

# Setting up a new device

### Update
```shell
sudo apt update
sudo apt upgrade
```

### Clone repo
```shell
git clone https://github.com/phizeroth/storybooth
```

### Increase GPU memory
```shell
sudo raspi-config
```
- Select Performance Options
- Select GPU Memory
- Change to 256

### Update hostname
Go to Raspberry Pi Configuration from Preferences menu, update hostname to `storybooth_#`, replacing `#` with the device number.

## Google OAuth

### Install PyDrive
```shell
pip3 install pydrive
```

### Get OAuth credentials

#### Extract secrets
```shell
gpg keys.tar.gpg
tar -xvf keys.tar
```

#### API client ID
Go to [Google Cloud Platform | APIs and Services | Credentials](https://console.developers.google.com/apis/credentials?project=story-booth)

#### Service account credentials
Go to [Google Cloud Platform | IAM | Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts?project=story-booth&supportedpurview=project)

### Destination configuration
Edit `id.json`
```json
{
  "team_drive_id": <stays the same>,
  "location": <device's assigned location>,
  "folder_id": <folder id to upload to>
}
```
The folder id comes from the end of the Drive folder url, e.g. `https://drive.google.com/drive/folders/` _`1dq1SCmszEyART3VkqxKUgvRiGlUA8x_8`_


## Startup configuration
Make `run.py` executable:
```shell
sudo chmod +x /home/pi/storybooth/run.py
```
Place `storybooth.service` into `/lib/systemd/system`

Reload systemctl and reboot:
```shell
sudo systemctl daemon-reload
sudo systemctl enable storybooth.service
sudo reboot
```

## Remote configuration
- Download and install TeamViewer:
https://www.teamviewer.com/en-us/download/raspberry-pi
- Open TeamViewer from the system tray and log in to account.

## Other
- Set `/home/pi/storybooth/desktop.png` to background image
- Right-click Trash icon on desktop and "Remove from desktop"
- Right-click panel, select Panel Settings, Advanced tab, check "Minimize panel when not in use"