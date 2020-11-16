#BASE ISO

#STEPS FOR INSTALLATION
#for PC

su

ip a

ip link set wlan0 up # say wlan0 is my wifi adaptor

rfkill unblock wifi #if above commands results as error

ip link set wlan0 up

connmanctl

scan wifi

services

agent on

connect <wifi-id>


#passwd

quit
##########################################################
#for VM
##########################################################

lsblk

fdisk /dev/sda
  g
  
  n
  
  >
  
  >
  
  +200m
  
  t
  
  uefi
  
  n
  
  w
  
  q

mkfs.fat -F32 /dev/sda1

mkfs.ext4 /dev/sda2

mount /dev/sda2 /mnt

mkdir /mnt/boot

mount /dev/sda1 /mnt/boot

basestrap /mnt base elogind-runit git linux <DRIVERS> {linux-headers}{dkms}

fstabgen -U /mnt >> /mnt/etc/fstab

artools-chroot /mnt

################# with BSPWM  ###############################

git clone https://github.com/XA-DE/bspartix.git

cd bspartix

sh install

exit

umount -R /mnt

reboot

ln -s /etc/runit/sv/NetworkManager /run/runit/service/NetworkManager
