+++
date = '2025-06-06T22:16:42-04:00'
draft = false
title = 'Sub-microsecond Time Synchronization Using PPS'
+++

## Context

This is a side quest while trying to build my own [Kraken SDR](https://github.com/krakenrf/krakensdr_docs/wiki) using 5x RTL-SDR. I was reading about how to achieve phase coherence, stumbled on PPS synchronization and figured it'd be simple to implement. Not so much at first, because I was using a UART GPS module with the TTL dongle. Then I saw my small GPS module for the [Joseph Hewitt's Wardriver Board](https://wardriver.uk/) uses TTL and PPS pinouts, so a few minutes later and here we are!

## Implementation

The host is synchronized to GPS time via a USB GPS/GNSS receiver sending NMEA and PPS signals. The NMEA sentences are received via SHM (shared memory) from gpsd, and the PPS signal is used as the primary synchronization reference through Chrony. The system operates as a stratum 1 NTP source, which is the highest precision level that a computer can realistically achieve.

## GPSD Configuration

Edit the file `/etc/default/gpsd`:

* Add the device path to the serial converter dongle:
    ```
    DEVICES="/dev/ttyUSB0"
    ```

* Add the following options to use readonly mode, and start polling right away:
  
    ```
    GPSD_OPTIONS="-b -n"
    ```

## Chrony Configuration

Edit the file `/etc/chrony/chrony.conf`:

* Comment out any default `pool` or `server` lines, or append the `noselect` option to keep the NTP sources for comparison, but not synchronization.

* Add the lines below to use shared memory to receive NMEA sentences from gpsd:

    ```
    refclock SHM 0 offset 0.5 delay 0.2 refid NMEA noselect
    refclock SHM 1 refid PPS lock NMEA
    ```

## Chrony Commands

`chronyc sources` - Display sources, offsets, and which source may be selected for synchronization. (`#* PPS` should be displayed when PPS is working)
* Add `-v` to get column definitions

`chronyc sourcestats` - Display additional offsets to the basic `sources` command.
* Add `-v` to get column definitions

`chronyc tracking` - Display system time, detailed offsets and sync status.

## PPS Tools

Kali Linux has `ppscheck` installed by default, and can be used to test if the `/dev/pps0` device is working properly:

`ppscheck /dev/pps0`

Alternatively, you can install additional PPS tools helpful with debugging PPS using `sudo apt install pps-tools`:

`ppstest /dev/pps0`

## ATGM336H GPS Breakout Module

### Component List

* ATGM336H GPS Breakout Module [Amazon](https://www.amazon.com/dp/B09LQDG1HY)
* Waveshare Industrial USB Dongle to TTL (FT232RNL) [Amazon](https://www.amazon.com/dp/B087RJ7X32) - [Waveshare Wiki](https://www.waveshare.com/wiki/USB_TO_TTL)
* USB extension cable (optional, but recommended for stress relief and to improve GPS antenna placement if using a short antenna)

### Wiring Diagram

*Pictures coming soon*

Make sure you change the voltage switch to 5V configuration, 3V3 doesn't seem to supply enough current to power the module - even though it's listed as using up to 3.6V. There is a capacitor to regular power, so providing 5V won't damage the module.

| ATGM336H      | Waveshare Dongle |
| ------------- | ---------------- |
| RX            | TX               |
| TX            | RX               |
| GND           | GND              |
| VCC           | VCC              |
| PPS           | DCD              |