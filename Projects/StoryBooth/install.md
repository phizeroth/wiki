---
title: Software Setup
description: 
published: true
date: 2022-02-11T20:40:47.468Z
tags: 
editor: markdown
dateCreated: 2022-02-11T20:40:47.468Z
---

# Setting up a new device

### Update
```bash
sudo apt update
sudo apt upgrade
```

### Clone repo
```bash
git clone https://github.com/phizeroth/storybooth
```

### Increase GPU memory
```bash
sudo raspi-config
```
- Select Performance Options
- Select GPU Memory
- Change to 256

## Google OAuth

### Install PyDrive
```bash
pip3 install pydrive
```

### Get OAuth credentials
Go to https://console.developers.google.com/apis/credentials?project=story-booth and create a credential. Download the json and transfer to the Storybooth folder on the RPi. (https://file.io can be handy.)

