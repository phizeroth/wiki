---
title: SmartThings Button
description: Small, multi-function Zigbee switch
published: true
date: 2023-03-25T21:31:35.916Z
tags: iot, hass, smartthings, zigbee
editor: markdown
dateCreated: 2020-08-06T21:22:00.320Z
---

![smartbutton_01_0000400.png](/smartbutton_01_0000400.png){.align-abstopright}

*[RFD]: Reduced-function device (does not extend mesh)

|-|-|
![smartbutton_01_0000400.png](/smartbutton_01_0000400.png)||
Protocol|Zigbee (RFD)
Power|Battery<br>CR2450 3V
Inputs|single press<br>long press<br>double press
Sensors|battery level<br>temperature
{.float-right}

## Setup

After pairing with deCONZ, the device shows up in HassOS as a "button" by manufacturer Samjin, with two entities:
- sensor.button_battery_level
- sensor.temperature

In order to capture the button as a trigger, first go to Developer Tools > Events, subscribe and listen to `deconz_event` and press the button to get the `id`. DeCONZ has been known to change a device's `id` after a reboot, so for extra certainty, use the `unique_id` instead.

```json
{
    "event_type": "deconz_event",
    "data": {
        "id": "button_2",
        "unique_id": "28:6d:97:00:01:0d:b7:a4",
        "event": 1002
    },
    "origin": "LOCAL",
    "time_fired": "2020-08-04T03:11:33.404795+00:00",
    "context": {
        "id": "2d7ea8c3001446adade540df2b7715bb",
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
  id: button_2
```

### Available events

action | event id
:-|-:
long press   | 1001
single press | 1002
double press | 1004

## References
[Manual (pdf)](https://support.smartthings.com/hc/en-us/article_attachments/360002610923/IOT_US_Button_QSG.pdf)
[Samsung SmartThings Button](https://www.samsung.com/us/smart-home/smartthings/buttons/samsung-smartthings-button-gp-u999sjvleaa/)
[Buy on Amazon](https://www.amazon.com/gp/product/B07F8ZFFQK)

