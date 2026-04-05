
2026-03-21 10:08

Tags: [[Proxmox]] [[Homelab]]

# Proxmox Mount Drives
You might want to keep your OS on an SSD but have a bulky memory such as a HDD to store media on. Then we will need to mount that HDD so it is available for our VM, the SSD is already present since installation.

### Setup
**Step 1: Find the full ID String**

Run this command on your Proxmox Node Shell (not the VM):
Bash
````
# sdb will be whatever is present in the proxmox home node
# it is the port connected to your desired drive you want to mount
ls -l /dev/disk/by-id | grep sdb
`````

You are looking for the line that starts with ata- and contains your serial Z9A4ZM5J. It will look something like this:
ata-ST8000DM004-2CX188_Z9A4ZM5J

**Step 3: Set it using the ID**

Now, plug it back in using the full path you found in Step 1:
Bash
````
# Replace 'ata-ID-HERE' with the actual string from Step 1
qm set 104 -scsi1 /dev/disk/by-id/ata-ID-HERE
````

**Step 4: Verify in Ubuntu**

Now, jump back into your Ubuntu VM (MobaXterm) and check the connection:
Bash

````
lsblk
`````

##### Now for the Ubuntu Particioning mounting
**Get the UUID**

We need the "fingerprint" of that partition (sda1) for the auto-mount settings. Run this:
Bash
````
sudo blkid /dev/sda1
`````

Copy the text inside the quotes for UUID="..." (e.g., 550e8400-e29b-41d4-a716-446655440000).
**Create the Mounting Point**

We need to create the folder where this drive will "live" in your file system.
Bash
````
sudo mkdir -p /mnt/data
`````

**Make it Permanent (The fstab file)**

If we don't do this, the drive will disappear every time you reboot.

**Open the configuration file:**
Bash
````
sudo nano /etc/fstab
`````

Arrow down to the very bottom and add this new line (replace the UUID with yours):
Plaintext

UUID=PASTE-YOUR-UUID-HERE  /mnt/data  ext4  defaults  0  2

(Note: If this drive was previously used in Windows, change ext4 to ntfs-3g. If it's empty/new, stick with ext4).

**Run this command. It "peeks" at the drive headers to see what's actually there:**
Bash

````
sudo lsblk -f /dev/sda
`````
I have xfs
# References
