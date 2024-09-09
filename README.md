# OpwnWRT_KVM_aarch64

Deploying OpenWRT on Orangepi Zero 3 as Guest OS.  
  Guest root will be a host disk partition.  

Prerequirements - kernel with virtualosation enabled.  
Here is a link to working kernel, compiled wit an orangepi-build  system.  
https://u.pcloud.link/publink/show?code=kZBjoO0Z0N6DdHilOAyiT3Vnb4u0nRJ2WBxk  
Patches about I2S3 audio output are included too.  



  Check OpenWrt release https://downloads.openwrt.org/releases/23.05.3/targets/armsr/armv8/  
  There are two files needed - generic-kernel.bin ( kernel image ) and  
  generic-ext4-rootfs.img.gz ( root filesystem ). Wget it both.  
  Exact names are "openwrt-23.05.4-armsr-armv8-generic-kernel.bin" and  
  "openwrt-23.05.4-armsr-armv8-generic-ext4-rootfs.img.gz" .  
  Gunzip the second one.  
  ''' $ gunzip openwrt-23.05.4-armsr-armv8-generic-ext4-rootfs.img.gz '''
  
  
    .. tbc ..
    
