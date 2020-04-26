# -*- mode: ruby -*-
# vi: set ft=ruby :

# you're doing.
Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/eoan64"
  config.vm.box = "generic/ubuntu1910"
  
  config.vm.provider "vmware_fusion" do |v|
    v.clone_directory="/Volumes/FastExtDisk/vmware/"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    echo "Remove previous jail"
    umount chroot_jail/proc   
    rm -rf chroot_jail
    echo "Copy libraries to run /bin/ls command"
    mkdir chroot_jail
    mkdir -p chroot_jail/lib/x86_64-linux-gnu/
    mkdir -p chroot_jail/lib64
    mkdir -p chroot_jail/bin
    mkdir -p chroot_jail/proc
    cp -pP /lib/x86_64-linux-gnu/libselinux* \
          /lib/x86_64-linux-gnu/libc* \
          /lib/x86_64-linux-gnu/libpcre* \
          /lib/x86_64-linux-gnu/libdl*  \
          /lib/x86_64-linux-gnu/libpthread* \
          /lib/x86_64-linux-gnu/ld* \
           /lib/x86_64-linux-gnu/libprocps* \
           /lib/x86_64-linux-gnu/libtinfo* \
           /lib/x86_64-linux-gnu/libsystemd* \
           /lib/x86_64-linux-gnu/librt* \
           /lib/x86_64-linux-gnu/liblz* \
           /lib/x86_64-linux-gnu/libgcrypt* \
           /lib/x86_64-linux-gnu/libgpg-error* \
           /lib/x86_64-linux-gnu/libmount* \
           /lib/x86_64-linux-gnu/libblkid* \
          chroot_jail/lib/x86_64-linux-gnu/
    cp -pP /lib64/ld-linux-x86-64.so.2 chroot_jail/lib64/ld-linux-x86-64.so.2
    cp -p /bin/ls chroot_jail/bin/
    cp -p /bin/top chroot_jail/bin/
    cp -p /bin/ps chroot_jail/bin/
    cp -p /bin/bash chroot_jail/bin/

   echo "Mount proc in the chroot_jail"
   mount proc -t proc chroot_jail/proc 
  SHELL
end
