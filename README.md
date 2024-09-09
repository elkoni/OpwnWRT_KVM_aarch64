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
  ``` $ gunzip openwrt-23.05.4-armsr-armv8-generic-ext4-rootfs.img.gz ```  
  
  Create a disk partition of size 512M - 1G. Note a partition id under the /dev/disk/by-id/ .  
  Block copy the uncompressed image to this partition.  
  ``` $ dd if=openwrt-23.05.4-armsr-armv8-generic-ext4-rootfs.img of=</dev/disk/by-id/<partition_id bs=1M oflag=direct status=progress ```  
  The rootfs is about 100M. It needs to fit a partition.  
  ``` $ resize2fs /dev/disk/by-id/<partition_id> ```  
  Create soft link for a kernel.  
  ``` ln -s openwrt-23.05.4-armsr-armv8-generic-kernel.bin generic-kernel.bin ```  
  Test it with:  
  ```
 qemu-system-aarch64 -enable-kvm -m 256M -smp 2 \
-cpu host -M virt -nographic \
-kernel generic-kernel.bin \
-append "root=fe00" \
-blockdev driver=host_device,node-name=hosthdd0,cache.direct=on,filename="/dev/disk/by-id/<partition_id>" \
-blockdev driver=raw,node-name=hd0,file=hosthdd0 \
-device virtio-blk-pci,drive=hd0 \
-serial unix:console.sock,server,nowait ```  
