# ConnectX-3-Proxmox
Packages and description on how to use Mellanox Connect-X3 Ethernet Cards on Proxmox:

I had quite the time trying to get my ConnectX-3 40GbE / 56GbIB cards working under proxmox, so hopefully this can help clarify the connfig a bit with information i've pieced together from various articles:

Note: This guide is based off Proxmox 8.3 but past versions **should** work as well as future versions.

## Disclaimer
I am not responsible for any damage occuring to cards when flashing, **ENSURE YOU HAVE CORRECT FIRMWARE VERSIONS DOWNLOADED IF YOU DECIDE TO MANUALLY FLASH**

### Installing Packages
To start, you should install Mellanox tools:
'''
apt-get update
apt install mstflint
'''
This will install the open-source version of Mellanox's MST tool, which I will use later to flash firmware if online update does not work.
First start by upgrading card firware ((Another guide available here)[https://that.guru/blog/updating-mellanox-connectx-3/]), or mstconfig won't be able to query if the FW version is lower than 2.31.5000
'''
mstflint -q 01:00:0 q
'''
The above will query the PCIe device for the IDs. The field we're interestred in is "PSID", which will give an ID we can use to identify the correct firmware to download. 
