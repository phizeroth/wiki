---
title: Minecraft Java Server Setup
description: Setting up a Minecraft Java server on Linux
published: true
date: 2023-07-21T16:56:51.904Z
tags: linux, server, minecraft
editor: markdown
dateCreated: 2023-07-21T16:56:51.904Z
---

## User setup
Best practice is to run the Minecraft server from a dedicated user with no sudo access.
```sh
sudo useradd mc
su - mc
```

Make a Minecraft directory
```sh
mkdir minecraft
```

For convenience, I added my main user to the `mc` group so I could more easily access the server folder/files
```sh
su - phi
sudo usermod -aG mc phi
chmod g+ws /home/mc
```