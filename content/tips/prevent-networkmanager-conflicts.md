+++
date = '2025-04-29T10:46:10-04:00'
draft = false
title = 'Prevent NetworkManager Conflicts'
+++

Different methods to exclude interfaces from NetworkManager's control:

1. Create the file: `/etc/NetworkManager/conf.d/99-unmanaged-devices.conf`
2. Add the required text based on the list below.
3. Reload the NetworkManager service: `systemctl reload NetworkManager`

## Exclude by Interface
```
[keyfile]
unmanaged-devices=interface-name:enp1s0
``` 

## Exclude by MAC address

```
[keyfile]
unmanaged-devices=mac:52:54:00:74:79:56
```

## Exclude by Device Type (wifi, ethernet, etc.)

```
[keyfile]
Unmanaged-devices=type:wifi
```

## Exclude multiple devices

```
[keyfile]
unmanaged-devices=interface-name:enp1s0;interface-name:enp7s0
```

Ref: [Red Hat Documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/configuring-networkmanager-to-ignore-certain-devices_configuring-and-managing-networking)