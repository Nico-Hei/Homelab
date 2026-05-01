# Samba
I am using Samba to locally host two file shares.

The first share is called **"Longterm"** and is used for files I do not need to
access regularly.
The second share is called **"Workspace"** and is used for everything I am
currently working with.

I use one important environment variable for both shares:
`SHARE=Longterm;/Longterm;yes;no;no;nico;nico`

Which translates to:
`name=Longterm;path=/Longterm;browse=yes;readonly=no;guest=no;users=nico;admins=no`

Both shares are stored on my RAID pool and get snapshotted every night.

My main user is hardcoded as `USER=nico;${SAMBA_PASSWORD}`. There is currently
no web dashboard for managing users. If you need to add users without restarting
the container, I would recommend a solution like OpenMediaVault instead.

The shares are accessible from any device. On Windows, I have them mounted as
network drives. On Linux, you can access them as follows:
`smb://nicoshl.de/Workspace`

[![Static Badge](https://img.shields.io/badge/Go%20back-B0B0B0?style=for-the-badge)](../../README.md)
