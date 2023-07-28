---
title: Pheunorbia Server Basics
description: 
published: true
date: 2023-07-28T16:02:16.992Z
tags: 
editor: markdown
dateCreated: 2023-07-27T19:05:01.677Z
---

# Access
Remote shell:
```bash
ssh -p 60022 mc@pheunorbia.phiz.io
```
> User `mc` has no sudo access and a locked password.
{.is-info}


## Server location
`/home/mc/pheunorbia/`
aka `~/pheunorbia`

# Server management

## `screen`
Pheunorbia uses [screen](https://linuxhandbook.com/screen-command/) to cleanly run the server in a background process that can be "attached" or "detached" from any terminal window, and closing/disconnecting a terminal window will not kill the server.

To **r**eattach/**r**esume the server screen:
```bash
screen -r
```
If it says a screen is already attached elsewhere, this means it is open in another terminal. To **d**etach the screen from wherever it is and **r**eattach to your terminal:
```bash
screen -dr
```

While the server is running, the screen can be detached by the command `Ctrl-A, D`

To scroll, use `Ctrl-A, Esc` to enter copy mode, then `PgUp` and `PgDn`.

## Start server
From the `~/pheunorbia` directory:
```bash
./start.sh
```
The current startup command contained in `start.sh` is:
```bash
screen -dmS minecraft java -Xmx2048M -Xms2048M -jar paper.jar --world phnord --nogui
```

## Stop server
If the server is running in your terminal, `Ctrl-C` or entering the command `stop` will gracefully shut down the server.

## Back up server
Stop the server first before backing up.

In `~/pheunorbia`, run the following script:
```bash
./backup.sh
```

## Update PaperMC
Check current and previous version:
```bash
cat version_history.json
```
> Stop the server before updating!
{.is-warning}

Check https://papermc.io/downloads/paper for the latest Paper version and build #.
Run the update script, and enter version and build # at the prompts:
```bash
./update.sh
```
This script will `curl` the given version and build of Paper and replace the current `paper.jar` file.
