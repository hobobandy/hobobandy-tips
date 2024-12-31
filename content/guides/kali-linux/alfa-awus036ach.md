+++
date = '2024-12-31T06:38:15-05:00'
draft = false
title = 'Alfa AWUS036ACH'
+++

## References

* [Alfa's RTL8812AU Support Page](https://docs.alfa.com.tw/Support/Linux/RTL8812AU/)
* [morrownr's Driver](https://github.com/morrownr/8812au-20210820)
* [aircrack-ng's Driver](https://github.com/aircrack-ng/rtl8812au)

## Driver Installation

> [!NOTE]
> I prefer to use the [morrownr's driver](https://github.com/morrownr/8812au-20210820) since it's a community-driven project.

1. Install the DKMS and Kernel headers package:  
   `sudo apt-get install dkms linux-headers-$(uname -r) bc`
2. Clone the repository:  
   `git clone https://github.com/morrownr/8812au-20210820.git`
3. Change to the cloned directory:  
   `cd 8812au-20210820`
4. Install the driver:  
   `sudo make dkms_install`
5. Run the installation script as a superuser - follow the instructions:  
   `sudo ./install-driver.sh`