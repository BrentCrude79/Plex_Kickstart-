Kickstart file for Red Hat Enterprise Linux Plex Server Build 

Features:
Hardened Media server with SMB sharing, SSH access, and rootless podman containers for:
Plex
Sonarr
Radarr
Sabnzbd
Guardtowarr (monitoring)
WUD (container updates)

Requirements:

Red Hat Enterprise Linux ISO file (https://developers.redhat.com/products/rhel/download#downloadsbyrelease)
Red Hat Individual Developer Subscription (https://developers.redhat.com/articles/faqs-no-cost-red-hat-enterprise-linux)
Dell Optiplex Server with AMD APU (Intel also works, but requires a little tweaking) 
Internal NVME drive for operating system installation. **** WILL BE DESTROYED / ERASED WITHOUT PROMPTING DURING USB BOOT *** 
A media drive attached to the system by USB or SATA with at least 1.5 TB total space formatted as one of EXT4/BTRFS/NTFS/EXFAT
(optional) a USB backup drive

Install process:
Modify the ks.cfg wherever comments mention a variable to be changed which at minimum includes:
-IP address (subnet, DNS, gateway) and hostname paramaters
-Plex Claim Token (if porting a Plex configuration over)
-Radarr and Sonaar API Keys (or you'll have to configure Guardtowarr later)
-username and password

Follow the Ventoy instructions to create a Ventoy USB bootable disk. Then copy files to the USB bootable as follows:
/ (Ventoy Partition)
├── ISOs/
│   ├── rhel-x.x-x86_64-dvd.iso
├── kickstarts/
│   ├── ks.cfg (modified as stated above) 
Configure the BIOS to boot off the USB drive and then start the system with the USB connected to a high speed (blue) USB3.0 port (USB-C not reccomended)

The Anaconda installer upon boot will automatically:
-Format the NVME internal drive and install Red Hat minimual 
-Apply security hardening and firewall settings
-Install minimal necessary software 
-Mount the 1.5+ Tb drive as /Library 
-Share the /Library folder via SMB 
-Open SSH ports with Password and Certificate authentication ready 
-pull and spin up the containers for Plex, Sonarr, Radarr, Sabnzbd, WUD, and Guardtowarr 
-enable touchless automatic updates for everything 
