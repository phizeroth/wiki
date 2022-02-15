---
title: Development Notes
description: 
published: true
date: 2022-02-15T16:50:08.590Z
tags: 
editor: markdown
dateCreated: 2022-02-14T15:57:50.712Z
---

## Archive and encrypt secrets

Always encrypt secrets folder before committing to git if any auth files have been changed.

```shell
tar -cvf auth.tar auth/
gpg -c auth.tar
```