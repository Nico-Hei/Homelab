# Welcome to my 💫 Homelab 💫

## 1. History
I started building my homelab around 6 years ago when I bought my first Raspberry Pi.
Originally I wanted to use the Pi to host self-coded Discord bots, but soon realized
the endless possibilities of self-hosted software.
I started out using Raspberry Pi OS Lite and later switched to Ubuntu Server 20.04,
which I have been running ever since (now on 24.04).
I also used my newly learned skills to host Minecraft servers for me and my friends,
though on VPSs rather than locally.
After this I used a custom built pc as my server for a very long time(as found in README_OLD.md). 
Recently I switched to a pre built nas from ugreen as the energy costs of my server didnt corelate
with the power needed to run all my 24/7 homelab services.

## 2. OS
I am currently running TrueNAS Scale. I have never used a nas os before and wanted to use the server switch as a
possibility to make my life a little easierer regarding managing my required services. I also wanted to use this opportunity 
to learn a bit more about permission management using ACL's. I am still going to manage my docker services via shell not gui.

## 3. Hardware
**Prebuilt UGREEN DXP2800**
---
**CPU:** Intel N100 (4 cores, 4 threads @ 3.4GHz)

**RAM:** 8GB DDR5 (Single Stick from Samsung)

**Storage:**
  1. Random 256GB Samsung m.2 ssd i found in an old desktop
     > Boot drive, also used for storing snapshots.
  2. 2× Lexar NS100 1TB SATA SSDs
     > Configured as a RAID-1 mirror for redundant data storage.
 
## 4. TrueNAS
### 4.1 Permissions
#### 4.1.1 Users
1. "truenas_admin" (locked) default user
   Permissions:
     Full Admin 
3. "nico.admin" my admin user to configure everything
   Permissions:
     Full Admin 
4. "nico" my user (non admin) for share access
   Permissions:
     SMB Access
   Groups:
     files_access
6. "guest" used to access Public share
   Permissions:
     SMB Access
   
#### 4.1.2 Groups
1. files_access (Used to access my private file share)

### 4.2 Networking
#### 4.2.1 Static IP
In truenas network settings:
- Interface: enp2s0
- IP: 192.168.1.250/24
- Autoconfigure IPv6 disabled (Iam not going to use IPv6 in my private network anytime soon)
- DNS server: 192.168.1.1 (My routers dns server)
- Default gateway: 192.168.1.1

#### 4.2.2 Docker networks

### 4.3 Storage and Datasets
#### Storage
Pool using 2 storage ssds in Mirror(Raid-1) "CrazyBigStorage"

#### Datasets
1. "Public" (SMB preset) a non password protected share used to send rescources between my devices
  Permissions:
    NFS4_Open preset
1.2 "Files" (SMB preset) my private files which should only be accessabile through my own (non admin) account
  Permissions:
    NFS4_Restricted preset
    Groups:
      files_access (Full Control)
1.3 "Container" (Apps preset) used for my docker services

## 5. Todo
1. Email alerts
2. Change GUI port of truenas to be able to use port 80 specificly for Nginx Proxy Manager
   
---
If you have any questions about service configurations, errors you encountered
during setup, or recommendations for this repo, feel free to reach out via
the contacts on my [profile](https://github.com/Nico-Hei).
