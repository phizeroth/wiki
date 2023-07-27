---
title: Pheunorbia Server Basics
description: 
published: true
date: 2023-07-27T21:01:20.639Z
tags: 
editor: markdown
dateCreated: 2023-07-27T19:05:01.677Z
---

## Server location
`/home/mc/minecraft/pheunorbia`

## Server management
Pheunorbia uses [screen](https://linuxhandbook.com/screen-command/) to cleanly run the server in a background process that can be "attached" or "detached" from any terminal window, and closing/disconnecting from a terminal window will not kill the server.

### Start server
```bash
./start.sh
```
The current startup command contained in `start.sh` is:
```bash
screen -dmS minecraft java -Xmx2048M -Xms2048M -jar paper.jar --world phnord --nogui
```

### Stop server
If the server is running in your terminal, `Ctrl-C` or entering the command `stop` will gracefully shut down the server.

If the server was already running in another terminal:
```bash
systemctl stop minecraft
```

### Update PaperMC
Go to https://papermc.io/downloads/paper and download the new build. Copy to `/home/mc/minecraft/pheunorbia/paper.jar`