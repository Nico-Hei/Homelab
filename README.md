# Welcome to my 💫 Homelab 💫

## 1. History
I started building my homelab around 6 years ago when I bought my first Raspberry Pi.
Originally, I wanted to use the Pi to host self-coded Discord bots, but I soon realized
the endless possibilities of self-hosted software.
I started out using Raspberry Pi OS Lite and later switched to Ubuntu Server 20.04,
which I have been running ever since (now on 24.04).
I also used my newly learned skills to host Minecraft servers for me and my friends,
though on VPSs rather than locally.
After this, I used a custom-built PC as my server for a very long time (as found in README_OLD.md).
Recently, I switched to a pre-built NAS from UGREEN, as the energy costs of my server did not correlate
with the power needed to run all my 24/7 homelab services.

## 2. OS
I am currently running TrueNAS Scale. I have never used a NAS OS before and wanted to use the server switch as a
possibility to make my life a little easier regarding managing my required services. I also wanted to use this opportunity
to learn a bit more about permission management using ACLs. I am still going to manage my Docker services via the shell, not the GUI.

## 3. Hardware
**Prebuilt UGREEN DXP2800**

---

**CPU:** Intel N100 (4 cores, 4 threads @ 3.4GHz)

**RAM:** 8GB DDR5 (single stick from Samsung)

**Storage:**
1. Random 256GB Samsung M.2 SSD I found in an old desktop
   > Boot drive, also used for storing snapshots.
2. 2× Lexar NS100 1TB SATA SSDs
   > Configured as a RAID-1 mirror for redundant data storage.

## 4. TrueNAS

### 4.1 Permissions

#### 4.1.1 Users

1. "truenas_admin" (locked) default user  
   Permissions:
   Full Admin

2. "nico.admin" my admin user to configure everything  
   Permissions:
   Full Admin

3. "nico" my user (non-admin) for share access  
   Permissions:
   SMB Access  
   Groups:
   files_access

4. "guest" used to access the Public share  
   Permissions:
   SMB Access

#### 4.1.2 Groups

1. files_access (used to access my private file share)

### Github Repo

To use the configuration files from this repository, I clone the repository to my server (~) using a GitHub Token. For each container, I use /mnt/CrazyBigStorage/Container/ServiceName as the storage path.

All container data is stored on a mirrored and regularly backed-up drive

For the Token i use following, minimal access, settings:
![TokenSettings](https://github.com/Nico-Hei/Homelab/blob/main/Images/GithubTokenSettings.png)

### 4.2 Networking

#### 4.2.1 Static IP

In TrueNAS network settings:

- Interface: enp2s0
- IP: 192.168.1.250/24
- Autoconfigure IPv6 disabled (I am not going to use IPv6 in my private network anytime soon)
- DNS server: 192.168.1.1 (my router's DNS server)
- Default gateway: 192.168.1.1

#### 4.2.2 GUI

In TrueNAS general settings:

- Web interface port: HTTP 80 -> 8080, HTTPS 443 -> 4443 (Nginx uses these ports)

#### 4.2.3 Docker Networks

My reverse proxy is the highest-level container in my homelab. It should be the only one that has exposed ports on the host, so I create its own network.

`docker network create r_proxy`

I can add networks to my docker-compose.yml files by adding the following structure:

```yaml
services:
  name:
  ...
  networks:
    - r_proxy

networks:
  r_proxy:
    external: true
```

Because of this network, Nginx can access every service via its container name.

Nginx is the only service with exposed host ports:

```yaml
services:
  nginx:
    ports:
      - "80:80"
      - "443:443"
```

Every other service shall only use container-internal ports:

```yaml
services:
  name:
    expose:
      - "3306"
```

Every service which requires sub-services like databases also receives its own internal network to communicate only with the sub-service.

For example:

```yaml
services:
  immich:
    networks:
      - r_proxy
      - immich_internal

  database:
    networks:
      - immich_internal
```

#### 4.2.4 Cloudflare (Domain)

I use Cloudflare to configure my local domains. In the past, I used it as a reverse proxy for WireGuard,
but in this installation, I will be switching from WireGuard to Tailscale.

- I create a new access token:
  1. Edit Zone-DNS Template
  2. Permissions: Zone, DNS, Edit
  3. Zone resources: Include, Specific Zone, nicoshl.de
  4. I then save my token as a password-protected note in Bitwarden

I configured the name servers of my domain to point to Cloudflare so that I can manage my domain through Cloudflare.

- DNS Entries:
  1. `Name: nicoshl.de Type: A Record Content: 192.168.1.250`
  2. `Name: * Type: CNAME Record Content: @` (@ = nicoshl.de, so *.nicoshl.de)

#### 4.2.5 Nginx Proxy Manager
Nginx Proxy Manager listens to the host ports:
80 (host) -> 80 (local, tcp) : http
81 (host) -> 81 (local, tcp) : web ui
443 (host) -> 443 (local, tcp) : https

#### 4.2.6 (Software) Firewall

### 4.3 Storage and Datasets

#### 4.3.1 Storage

Pool using 2 storage SSDs in a mirror (RAID-1): "CrazyBigStorage"

#### 4.3.2 Datasets

1. "Public" (SMB preset) a non-password-protected share used to send resources between my devices  
   Permissions:
   NFS4_Open preset

2. "Files" (SMB preset) my private files which should only be accessible through my own (non-admin) account  
   Permissions:
   NFS4_Restricted preset  
   Groups:
   files_access (Full Control)

3. "Container" (Apps preset) used for my Docker services

## 5. Todo

1. Email alerts

---

If you have any questions about service configurations, errors you encountered
during setup, or recommendations for this repo, feel free to reach out via
the contacts on my https://github.com/Nico-Hei
