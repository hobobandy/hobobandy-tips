+++
date = '2024-12-31T07:34:40-05:00'
draft = false
title = 'GPS Configuration'
+++

## Required Packages

> [!NOTE]
> `gpsd-tools` provides `cgps` which I use for status monitoring and troubleshooting.

1. Install required packages:  
   `sudo apt install gpsd gpsd-tools`
2. Enable the gpsd service:  
   `sudo systemctl enable gpsd`
3. Start the gpsd service:  
   `sudo systemctl start gpsd`
4. Check GPS device is working using cgps - if multiple devices, specify the device path:  
   `cgps` or `cgps /dev/ttyACM#`
5. If it doesn't work, check for device-specific instructions below.

## USB Dongles

### BU-353N

* [GlobalSat BU-353N Product Page](https://www.globalsat.com.tw/en/product-282348/USB-GPS-Receiver-BU-353N.html)

```
LED OFF: Receiver switch off
LED ON: No fixed, Signal searching
LED Flashing: Position Fixed
```

1. Edit the gpsd configuration file:  
   `sudo nano /etc/default/gpsd`
2. Add the following gpsd options:  
   `GPSD_OPTIONS="-b -n"`

> [!NOTE]
> These mandatory switches were identified by the wardriving community for the BU-353N to work properly. They enable read-only mode, and tell gpsd not to wait for a client before polling the GPS device.

### BU-353S4

* [GlobalSat BU-353S4 EOL Notice](https://www.globalsat.com.tw/en/product-199952/Cable-GPS-with-USB-interface-SiRF-Star-IV-BU-353S4-EOL.html)
* `lsusb` = `067b:2303 Prolific Technology, Inc. PL2303 Serial Port`
* `ls /dev` = `/dev/ttyUSB#`

```
LED OFF: Receiver switch off
LED ON: No fixed, Signal searching
LED Flashing: Position Fixed
```

1. Edit the gpsd configuration file:  
   `sudo nano /etc/default/gpsd`
2. Add the device path to the devices:  
   `DEVICES="/dev/ttyUSB#"`

### uBlox 7

* `lsusb` = `1546:01a7 U-Blox AG [u-blox 7]`
* `ls /dev` = `/dev/ttyACM#`
* gpsd udev rules creates `/dev/gps#`