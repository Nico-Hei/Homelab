# Welcome to my 💫 Homelab 💫

## 1. History
I started building my homelab around 6 years ago when I bought my first Raspberry Pi.
Originally I wanted to use the Pi to host self-coded Discord bots, but soon realized
the endless possibilities of self-hosted software.
I started out using Raspberry Pi OS Lite and later switched to Ubuntu Server 20.04,
which I have been running ever since (now on 24.04).
I also used my newly learned skills to host Minecraft servers for me and my friends,
though on VPSs rather than locally.

## 2. OS
I am currently running Ubuntu Server 24.04. I appreciate the stability of its
Debian base while also benefiting from the additional features it offers,
particularly for virtual machines.
Although Ubuntu Server has a slightly higher hardware overhead, this has not been
an issue as none of my services come close to exceeding what the hardware can handle.

## 3. Hardware
- **CPU:** AMD Ryzen 5 2400G
  > I originally used a Ryzen 7 2700, but switched to the 2400G for its integrated
  > GPU, which handles video encoding/decoding and removes the need for a dedicated
  > GPU for debugging. The 4-core/8-thread configuration handles my workload well
  > and is more power-efficient at idle.
- **Mainboard:** Biostar B450MX-S (AM4)
  > Chosen for its 4 RAM slots and 2 PCIe x16 lanes, leaving room for future
  > expansions such as additional network cards.
- **RAM:** Corsair Vengeance 16GB DDR4-3600
- **Storage:**
  1. Crucial P2 500GB NVMe SSD
     > Boot drive, also used for storing snapshots.
  2. 2× Lexar NS100 1TB SATA SSDs
     > Configured as a RAID-1 mirror for redundant data storage.
- **PSU:** DeepCool PF400 400W
  > Sufficient for the current setup with enough headroom for future additions
  > such as a dedicated GPU.
- **Case:** SilverStone Milo ML04
- **Hardware not currently in use:**
  - SAS Card
  - Blu-ray Drive
 
## 4. Network & Domain
## 5. Services [^services]
[![Static Badge](https://img.shields.io/badge/Homarr-Dashboard-FA5252?style=for-the-badge&logo=Homarr&logoColor=white)](./Services/Homarr/Homarr.md)
[![Static Badge](https://img.shields.io/badge/Cloudflare-DDNS-F38020?style=for-the-badge&logo=Cloudflare&logoColor=white)](./Services/Cloudflare/Cloudflare.md)
[![Static Badge](https://img.shields.io/badge/Backrest-Snapshots-3B3737?style=for-the-badge)](./Services/Backrest/Backrest.md)
[![Static Badge](https://img.shields.io/badge/Immich-Photos-4250AF?style=for-the-badge&logo=Immich&logoColor=white)](./Services/Immich/Immich.md)
[![Static Badge](https://img.shields.io/badge/Memos-Notes-E0D484?style=for-the-badge&logo=Note&logoColor=white)](./Services/Memos/Memos.md)
[![Static Badge](https://img.shields.io/badge/Nginx%20Proxy%20Manager-Reverse%20Proxy-F15833?style=for-the-badge&logo=Nginx%20Proxy%20Manager&logoColor=white)](./Services/NginxProxyManager/NginxProxyManager.md)
[![Static Badge](https://img.shields.io/badge/Radicale-Calendar%20%26%20Contacts-853C1E?style=for-the-badge&logo=Webpack&logoColor=white)](./Services/Radicale/Radicale.md)
[![Static Badge](https://img.shields.io/badge/Wireguard-VPN-88171A?style=for-the-badge&logo=Wireguard&logoColor=white)](./Services/Wireguard/Wireguard.md)
[![Static Badge](https://img.shields.io/badge/Samba-File%20Share-489A9C?style=for-the-badge)](./Services/Samba/Samba.md)
[![Static Badge](https://img.shields.io/badge/Vaultwarden-Password%20Manager-000000?style=for-the-badge&logo=Vaultwarden&logoColor=white)](./Services/Vaultwarden/Vaultwarden.md)
[![Static Badge](https://img.shields.io/badge/Cockpit-VM%20Manager-0066CC?style=for-the-badge&logo=Cockpit&logoColor=white)](./Services/Cockpit/Cockpit.md)

[^services]: Open service details by clicking on the service badge
## 6. Todo
- Setup docker networks between containers correctly, currently only the bridge and host network are being utilized.
- Setup Actual budget manager
- Setup Termux ssh manager

---
If you have any questions about service configurations, errors you encountered
during setup, or recommendations for this repo, feel free to reach out via
the contacts on my profile.

[![Static Badge](https://img.shields.io/badge/Profile-E36256?style=for-the-badge)](https://github.com/Nico-Hei)

