---
title: process management
description: 
published: true
date: 2021-09-07T19:29:03.335Z
tags: linux
editor: markdown
dateCreated: 2021-09-07T18:51:26.015Z
---

## List running processes

List all running processes: `ps aux`
More detailed process monitor: `top` or [`htop`](/Linux/utilities#resource-monitor)

## Kill processes
Kill process by PID: `kill [PID]`
Kill process by name: `killall [name]`

A specific kill signal can be sent, e.g. `kill -9 [PID]`. Enter `kill -l` for a list of all signals.

Signal | # | Effect
-|:-:|-:
SIGHUP | 1 | Hangup
SIGINT | 2 | Keyboard Interrupt
SIGKILL | 9 | Kill
SIGTERM | 15 | Terminate
SIGSTOP | 19 | Stop