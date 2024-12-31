+++
date = '2024-12-30T18:49:00-05:00'
draft = false
title = 'Initial Setup'
+++

## Common Steps

1. Download the Kali Linux installer from [the official Kali website](https://www.kali.org/get-kali/).
2. Use [Balena Etcher](https://etcher.balena.io/) to create a bootable USB install drive.
3. Plug the USB drive into the system and boot from it.
   * This step may need BIOS changes. (e.g. secure boot disabling, legacy mode activation)
4. Complete the installation as desired.
5. Login using the user account.
6. Open a `Terminal Emulator`.
7. Note the IP address:  
   `ifconfig`
8. Enable the SSH server service:  
   `sudo systemctl enable ssh`
9.  Perform a full system update - this will take a while:  
   `sudo apt update && sudo apt full-upgrade`
10. Reboot the system:  
    `sudo reboot`

## SSH

### Password Authentication

>[!CAUTION]
>This is not a recommended method of authentication, especially if your system is connected to the Internet. You should use SSH keys.

1. Edit the configuration file as a superuser:  
   `sudo nano /etc/ssh/sshd_config`
2. Uncomment the line:  
   `PasswordAuthentication yes`
3. Restart the SSH server:  
   `sudo systemctl restart ssh`
4. You may now logout, and remote into the system.
    * For Windows, I recommend [MobaXterm](https://mobaxterm.mobatek.net/) or [PuTTY](https://www.putty.org/).

### Key-based Authentication

*To be confirmed.*

## Headless Installation (RPi)

For a headless installation, and to have the system connect to a WiFi network automatically, add a `wpa_supplicant.conf` file to the first partition of the USB drive.

Generate the file using the following command on a different Linux system:  
`wpa_passphrase YOURNETWORK > wpa_supplicant.conf`

>[!CAUTION]
>Your user's shell history will now contain your WiFi network password, edit your shell's history file to remove it. (e.g. `~/.zsh_history`, `~/.bash_history`)