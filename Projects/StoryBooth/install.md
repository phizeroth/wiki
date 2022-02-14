---
title: New StoryBooth Device Setup
description: A guide for setting up a new completed StoryBooth device after first powering it on
published: true
date: 2022-02-14T19:43:33.305Z
tags: 
editor: markdown
dateCreated: 2022-02-11T20:40:47.468Z
---

## OS setup

### Update
```shell
sudo apt update
sudo apt upgrade
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

## Install StoryBooth application

### Clone repo
```shell
git clone https://github.com/phizeroth/storybooth
```

> After this point, all shell commands in these instructions assume you are in the /home/pi/storybooth folder.
{.is-info}

### Install dependencies

* Install [picam](https://github.com/iizukanao/picam) by following instructions at https://github.com/iizukanao/picam.
* Install [PyDrive](https://pythonhosted.org/PyDrive/index.html):
```shell
pip3 install pydrive
```

## Google OAuth

Extract secrets:
```shell
gpg auth.tar.gpg
tar -xvf auth.tar
rm auth.tar*
```

* API Client ID:
[Google Cloud Platform | APIs and Services | Credentials](https://console.developers.google.com/apis/credentials?project=story-booth)

* Service account credentials:
[Google Cloud Platform | IAM | Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts?project=story-booth&supportedpurview=project)

### Destination configuration
Edit `auth/folder.json` to assign the device to a particular site/location/purpose. This will set the folder which all the device's videos will upload to:
```json
{
  "team_drive_id": <stays the same>,
  "location": <name of device's assigned location>,
  "folder_id": <folder id to upload to>
}
```
The folder id comes from the end of the Drive folder url, e.g. `https://drive.google.com/drive/folders/` _`9dq1SCmsasj73VkqxKUgvRiKlUA3x_8`_


## Startup configuration
The StoryBooth program needs to automatically run at startup. To do so, use the included unit file to configure `systemd`:

* Make `run.py` executable:
```shell
sudo chmod +x run.py
```
* Place the unit file `asset/storybooth.service` into `/lib/systemd/system`.
```shell
cp asset/storybooth.service /lib/systemd/system/storybooth.service
```

* Reload systemctl and reboot:
```shell
sudo systemctl daemon-reload
sudo systemctl enable storybooth.service
sudo reboot
```

## Set up remote access
- Download and install TeamViewer:
https://www.teamviewer.com/en-us/download/raspberry-pi
- Open TeamViewer from the system tray and log in to account.

## Other
- Right-click desktop, Desktop Preferences, set background picture to `/home/pi/storybooth/asset/desktop.png`
- Right-click Trash icon on desktop and "Remove from desktop"
- Right-click panel, select Panel Settings, Advanced tab, check "Minimize panel when not in use"