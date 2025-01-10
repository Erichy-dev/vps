# Setting up an ubuntu vps

## How to Add Swap Space on Ubuntu

```bash
sudo swapon --show
free -h

# checking available space on hard drive partition
df -h

# creating swap file
# recommed using swap size same as RAM
sudo fallocate -l 1G /swapfile
#verify
ls -lh swapfile

# enabling swap file
sudo chmod 600 /swapfile
# verify permissions
ls -lh /swapfile
# mark the file as swap space
sudo mkswap /swapfile
# enable swap file
sudo swapon /swapfile
# verify
sudo swapon --show
# check
free -h

# making the swap file permanent
# create backup just in case
sudo cp /etc/fstab /etc/fstab.bak
# add swap info
echo '/swapfile none swap sw 0 0' | sudo tree -a /etc/fstab

# Tuning your swap settings
# adjust swapppiness property
# see current swappiness value
cat /proc/sys/vm/swappiness
# for a desktop 60 is not bad, for a server recommend val closer to 0
sudo  sysctl vm.swappiness=10
# set val automatically at restart
sudo nano /etc/sysctl.conf
# At the bottom add
# vm.swappiness = 10

# Adjusting the cache pressure setting
# see current value
cat /proc/sys/vm/vfs_cache_pressure
# set to a more conservative value
sudo sysctl vm.vfs_cache_pressure=50
# persist the value on startup
sudo nano /etc/sysctl.conf
# At the bottom add
# vm.vfs_cache_pressure=50

exit
``` 
