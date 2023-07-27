---
title: Pheunorbia Server Basics
description: 
published: true
date: 2023-07-27T21:55:10.765Z
tags: 
editor: markdown
dateCreated: 2023-07-27T19:05:01.677Z
---

## Access
To access,
```bash
ssh -p 60022 mc@pheunorbia.phiz.io
```

## Server location
`/home/mc/minecraft/pheunorbia`

## Server management

### Screen
Pheunorbia uses [screen](https://linuxhandbook.com/screen-command/) to cleanly run the server in a background process that can be "attached" or "detached" from any terminal window, and closing/disconnecting a terminal window will not kill the server.

To **r**eattach/**r**esume the server screen:
```bash
screen -r
```
If it says a screen is already attached elsewhere, this means it is open in another terminal. To **d**etach the screen from wherever it is and **r**eattach to your terminal:
```bash
screen -dr
```

### Start server
From `/home/mc/minecraft/pheunorbia`:
```bash
./start.sh
```
The current startup command contained in `start.sh` is:
```bash
screen -dmS minecraft java -Xmx2048M -Xms2048M -jar paper.jar --world phnord --nogui
```

### Stop server
If the server is running in your terminal, `Ctrl-C` or entering the command `stop` will gracefully shut down the server.

### Back up server
Stop the server first before backing up.
Compress `/home/mc/minecraft/pheunorbia/*` (except `cache` directory) to `/media/phi/Hoard/backup/minecraft/pheunorbia_[YYYY-mm-dd].tar.gz`

### Update PaperMC
Go to https://papermc.io/downloads/paper and download the new build. Copy to `/home/mc/minecraft/pheunorbia/paper.jar`