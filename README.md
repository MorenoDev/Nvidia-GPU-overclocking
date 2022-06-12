# Linux Nvidia GPU overclocking

### Install Nvidia drivers
```bash
sudo apt install nvidia-driver-510
sudo reboot
```

### Delete Xorg file

`sudo rm /etc/X11/xorg.conf`

### Enable overclocking
```bash
sudo nvidia-xconfig -a --cool-bits=28 --allow-empty-initial-configuration
reboot
```

### Set clocks
```bash
sudo -n nvidia-smi -i 0 --persistence-mode=1 # Sets persistent clocks
sudo nvidia-smi -i 0 -pl 130 # Sets power limit to 130 watts
nvidia-settings -c :0 -a '[gpu:0]/GPUGraphicsClockOffset[3]=-200' # Sets Core Clock to -200
nvidia-settings -c :0 -a '[gpu:0]/GPUMemoryTransferRateOffset[3]=2600' # Sets Memory Clocks to 2600 (1300x2)
```

# TROUBLESHOOTING

### Issue 1:
> ERROR: Error assigning value -200 to attribute 'GPUGraphicsClockOffset'  
> ERROR: Error assigning value 2600 to attribute 'GPUMemoryTransferRateOffset'  

Solution:  
```bash
sudo vi /etc/X11/Xwrapper.config
```

Add line: needs_root_rights = yes  
```bash
sudo reboot
```

[reference 1](https://wiki.archlinux.org/title/NVIDIA/Troubleshooting#Overclocking_not_working_with_Unknown_Error "reference 1")  
[reference 2](https://wiki.archlinux.org/title/Xorg#Rootless_Xorg "reference 1")  