+++
date = '2024-12-31T08:05:09-05:00'
draft = false
title = 'Enabling WLAN Monitor Mode'
+++

Not much else to say, for some reason my brain hasn't saved these commands.

```
sudo ip link set wlan# down
sudo iw dev wlan# set type monitor
sudo ip link set wlan# up
```