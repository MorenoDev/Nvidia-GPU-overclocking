# Linux Nvidia GPU overclocking

### Install Nvidia drivers
sudo apt install nvidia-driver-510
sudo reboot

### Delete Xorg file
sudo rm /etc/X11/xorg.conf

### Enable overclocking
sudo nvidia-xconfig -a --cool-bits=28 --allow-empty-initial-configuration
reboot

### Set clocks
sudo -n nvidia-smi -i 0 --persistence-mode=1 # Sets persistent clocks
sudo nvidia-smi -i 0 -pl 130 # Sets power limit to 130 watts
nvidia-settings -c :0 -a '[gpu:0]/GPUGraphicsClockOffset[3]=-200' # Sets Core Clock to -200
nvidia-settings -c :0 -a '[gpu:0]/GPUMemoryTransferRateOffset[3]=2600' # Sets Memory Clocks to 2600 (1300x2)

# TROUBLESHOOTING

Issue #1:
ERROR: Error assigning value -200 to attribute 'GPUGraphicsClockOffset'
ERROR: Error assigning value 2600 to attribute 'GPUMemoryTransferRateOffset'

Solution: 
sudo /etc/X11/Xwrapper.config
Add line: needs_root_rights = yes 

https://wiki.archlinux.org/title/NVIDIA/Troubleshooting#Overclocking_not_working_with_Unknown_Error
https://wiki.archlinux.org/title/Xorg#Rootless_Xorg