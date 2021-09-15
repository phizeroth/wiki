---
title: Philips Hue dimmer switch
description: 
published: true
date: 2021-09-15T22:23:42.974Z
tags: 
editor: markdown
dateCreated: 2021-06-13T15:49:46.103Z
---

![white-philips-dimmers-458141-64_1000.jpg](/IoT/white-philips-dimmers-458141-64_1000.jpg){.align-abstopright}

## Overview

- **Protocol**
  - [Zigbee](https://en.wikipedia.org/wiki/Zigbee)
    - Reduced-function device (RFD), does not extend mesh

- **Power**
  - Battery (CR2450 3V)

- **Features**
  - inputs
    - single press
    - long press
  - sensors
	  - battery level

## Setup

In order to capture the button as a trigger, first go to Developer Tools > Events, subscribe and listen to `deconz_event` and press the button to get the `id`. DeCONZ has been known to change a device's `id` after a reboot, so for extra certainty, use the `unique_id` instead.

```json
{
    "event_type": "deconz_event",
    "data": {
        "id": "dimmer_switch",
        "unique_id": "00:17:88:01:03:c9:a8:04",
        "event": 1002,
        "device_id": "4060ab143b0f4a3f44d22f8c9b0c6716"
    },
    "origin": "LOCAL",
    "time_fired": "2021-06-13T15:42:32.715256+00:00",
    "context": {
        "id": "b6cb9c24da30d120c7e9135b69268972",
        "parent_id": null,
        "user_id": null
    }
}
```

Then set up an automation with an event trigger such as:
```yaml
platform: event
event_type: deconz_event
event_data:
  event: 1002
  id: dimmer_switch
```

### Available events
 
#### deCONZ `event`

action | ON | DIM UP | DIM DN | OFF
:-|-|-|-|-:
single press   | 1000 | 2000 | 3000 | 4000
single release | 1002 | 2002 | 3002 | 4002
long press | 1001 | 2001 | 3001 | 4001
long release | 1003 | 2003 | 3003 | 4003

 
#### ZHA `command`

Button event data in ZHA works in a different way from deCONZ. There is a `command` which combines two `args`: `button` and `press_type`.

| `button` options: | `press_type` options:
:-|-|-:
on   | press
up   | short_release
down | long_release
off  | double_press
     | triple_press
     | hold      

A `command` will be referenced in the format `[button]_[press_type]`, e.g. `on_press`, `down_short_release`.

## References
[Buy on Amazon (new model)](https://www.amazon.com/Philips-Hue-Installation-Free-Exclusively-562777/dp/B08W8GLPD5/)

