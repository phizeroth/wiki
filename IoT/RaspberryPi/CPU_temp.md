---
title: CPU temp
description: 
published: true
date: 2021-09-06T19:07:52.962Z
tags: rpi
editor: markdown
dateCreated: 2021-09-06T19:07:52.962Z
---

# CPU temperature
### vcgencmd
The built-in utility `vcgencmd` can be used to read the CPU temperature on the Raspberry Pi.

```shell
vcgencmd measure_temp
```

For a convenient shortcut command such as `temp`, add to your `~/.bash_aliases` file:
```bash
alias temp='/opt/vc/bin/vcgencmd measure_temp'
```

### References
https://elinux.org/RPI_vcgencmd_usage
https://www.nicm.dev/vcgencmd/