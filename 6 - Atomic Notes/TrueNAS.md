
2026-03-21 11:11

Tags: [[Homelab]]

# TrueNAS
When you are having a single hardware device such as a HDD and multiple VMs wants to mount it there is a problem and you could get data corruption if they both want to write to the same location. This makes it necessary to have some kind of NAS (Network attached storage). 

You will host your mounted disks on a lightweight VM and will distribute and connect via ip to the other VMs that want this data.

#### Setup
**Run this on the Proxmox Node Shell**
````
qm set 105 -scsi1 /dev/disk/by-id/ata-ST1000DM003-1SB102_Z9A4ZM5J
`````
105 being your machine id and the ata-... coming from the connected HDD/SSD

truenas_admin is the username when logging into the TrueNAS ip visible in the console. It is accessible through the web.

**Creating a new pool**
Through the web gui access Storage and create a new pool. Use Stripe if you dont want double redundancy with dual HDDs. 

I also had to go into Proxmox and give the 

**Setup in TrueNAS WEB GUI**
Go to storage and Create pool. 
Create a media folder with the add dataset.

**Mount the TrueNAS disks in respective VMs**
````
# 1. Install the NFS tool
sudo apt update && sudo apt install nfs-common -y

# 2. Create a folder to view your big drive
sudo mkdir -p /mnt/storage

# 3. Mount it (Replace 192.168.1.X with your TrueNAS IP)
sudo mount -t nfs 192.168.1.X:/mnt/Main_Storage/Media /mnt/storage
````

### General Disk space commands
Command to show occupied space:

````
df -h /
`````

**Remove Ghost Data**
When you remove data form a disk proxmox does not recognize it and if you want to clean up that data run this command:

````
sudo fstrim -av
`````
# References
