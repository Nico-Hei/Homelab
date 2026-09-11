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
 
**TrueNAS setup:**


---
If you have any questions about service configurations, errors you encountered
during setup, or recommendations for this repo, feel free to reach out via
the contacts on my [profile](https://github.com/Nico-Hei).
