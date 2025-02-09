+++
date = '2025-02-08T17:25:31-05:00'
draft = false
title = 'Compiling Kismet on Kali 2024.4'
+++

## Default Configuration

* To use the default `./configure` command, these are the required packages:

```bash
sudo apt install libpcre2-dev libsqlite3-dev libssl-dev pkgconf libwebsockets-dev libpcap-dev libnm-dev libnl-3-dev libnl-genl-3-dev libusb-1.0-0-dev libbtbb-dev librtlsdr-dev libmosquitto-dev libsensors-dev 
```

## Datasource-specific

* `rtl-433` package is already installed on a default Kali installation.
* `libubertooth-dev` package is required for Ubertooth support.

## Additional Options

* For full debug logs, add the `libdw-dev` package.

| Switch | Required Package |
| ----------- | ----------- |
| --enable-bladerf | libbladerf-dev |
| --enable-wifi-coconut | none | 
| --enable-btgeiger --enable-python-tools | none |