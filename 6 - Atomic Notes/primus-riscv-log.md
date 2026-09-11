
2026-04-08 01:11

Tags: [[Project primus-risc-v]]

# primus-riscv-log

### 7/4 -26
Implemented branch prediction and fixed a lot of timing, like when the signals was not gated properly and also some signals were delayed because of the forwarding. Now i have a functional core which can run the fibbonacci sequence program.

Also implemented the UART driver to load the bootloader program so i do not have to generate a new bitstream each time.

I have a new plan: 
![[Pasted image 20260408011426.png]]

Installed toolchain for compiling programs: 
```
sudo apt install gcc-riscv64-unknown-elf binutils-riscv64-unknown-elf
```

To compile the bootload image:
```
  cd /home/deadlywhisp3r/proj/primus-risc-v/sw                                     
  make
  make disasm #prints the code for you to view
  make install # copies to ip_user_files/mem_init_files/  
```

#### USB connection windows -> VM
To make the USB (serial connection for loading new programs) available use:
```
usbipd bind --busid 3-8
```
(you need to download it on your windows machine from https://github.com/dorssel/usbipd-win/)

On your VM install usbip
```
sudo apt-get install usbip hwdata
```
load the kernel module:
```
sudo modprobe vhci-hcd
```
I asked AI to make a script which automatically upon system boot loads the module and attaches the USBs. so i do not know if the load kernel is needed since it is in that script.
```
sudo bash ~/usbip-attach.sh
```

### load hazards
fix for load hazards
# References
