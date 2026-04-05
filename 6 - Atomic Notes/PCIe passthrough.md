
2026-03-20 23:41

Tags: [[Homelab]]

# PCIe passthrough
PCIe passthrough is necessary if we want to use the gpu in our virutal machines. This is very necessary for video transcoding when streaming your media from your ARR stack.

### Setup
Check if the graphics card is visible
````
lspci | grep -i nvidia
`````
How to fix the missing GPU:

    Go to the Proxmox Web Interface.

    Select your VM (arrstack) > Hardware tab.

    Check if you added the PCI Device. If not, click Add > PCI Device and select the GTX 1070.

    Important: Since we are using Q35 and OVMF, ensure these boxes are checked in the PCI device settings:

        All Functions

        ROM-Bar

        PCI-Express

    The "Host" setting: Go to VM > Hardware > Processors. Make sure the Type is set to host. This is mandatory for NVIDIA cards.
You need to enable direct accessing of hardware and you do that in the BIOS by going to ->
Advanced(f7) > Overclocking settings > OC Explore Mode (Expert) > CPU Features > VT-D -enabled

edit the grub file to tell the server to let the gpu talk directly to the VM. In the home node, enter the shell and type:

nano /etc/default/grub

Find the line:
GRUB_CMDLINE_LINUX_DEFAULT="quiet"

Change it to:
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"

Update and generate the new grub file
update-grub

Type: nano /etc/modules

Paste these four lines at the bottom:
````
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
`````

Make sure Proxmox does not take the Nvidia card for itself
````
echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf
echo "blacklist nvidia" >> /etc/modprobe.d/blacklist.conf
update-initramfs -u
`````
#### Install the Nvidia drivers
````
sudo apt update
`````
then install the 550 drivers:
````
sudo apt install nvidia-headless-550-server nvidia-utils-550-server -y
`````

#### If you are running Docker
To connect and let Docker containers use your GPU you need to run these commands:

We have the GPU, and we have Docker. Now we need to glue them together so your containers can "see" the GTX 1070.

**Run these 3 blocks in order:**

**1. Add the NVIDIA Repository:**

Bash

```
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

**2. Install the Toolkit:**

Bash

```
sudo apt update
sudo apt install -y nvidia-container-toolkit
```

**3. Tell Docker to use it:**

Bash

```
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

---

**Step 3: The "Magic" Test**

Once that's done, run this command to prove your Docker containers can transcode:

Bash

```
docker run --rm --runtime=nvidia --gpus all nvidia/cuda:12.2.0-base-ubuntu22.04 nvidia-smi
```
# References
