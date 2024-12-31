+++
date = '2024-12-31T07:34:40-05:00'
draft = false
title = 'GPS Configuration'
+++

## Required Packages

> [!NOTE]
> I install extra packages that offer tools I usually end up eventually using for troubleshooting or during development.

1. Install required packages:  
   `sudo apt install gpsd gpsd-clients gpsd-tools`

## USB Dongles

### BU-353N

* [GlobalSat BU-353N Product Page](https://www.globalsat.com.tw/en/product-282348/USB-GPS-Receiver-BU-353N.html)

1. Edit the gpsd configuration file:  
   `sudo nano /etc/default/gpsd`
2. Add the following gpsd options:  
   `GPSD_OPTIONS="-b -n"`

> [!NOTE]
> These mandatory switches were identified by the wardriving community for the BU-353N to work properly. They enable read-only mode, and tell gpsd not to wait for a client before polling the GPS device.

### uBlox 7

* `lsusb` = `1546:01a7 U-Blox AG [u-blox 7]`
* `ls /dev` = `/dev/ttyACM#`
* gpsd udev rules creates `/dev/gps#`

### BU-353S4

* [GlobalSat BU-353S4 EOL Notice](https://www.globalsat.com.tw/en/product-199952/Cable-GPS-with-USB-interface-SiRF-Star-IV-BU-353S4-EOL.html)
* `lsusb` = `067b:2303 Prolific Technology, Inc. PL2303 Serial Port`
* `ls /dev` = `/dev/ttyUSB#`
* Plug and play!