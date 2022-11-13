# qemu-basic

u-boot:
        - Refer: https://u-boot.readthedocs.io/en/latest/board/emulation/qemu-arm.html
        - Check out code from git clone https://github.com/u-boot/u-boot.git
        - make qemu_arm_defconfig CROSS_COMPILE=arm-linux-gnueabi-
        - make CROSS_COMPILE=arm-linux-gnueabi-
        - qemu-system-arm -machine virt -nographic -bios u-boot.bin -device usb-ehci,id=ehci

kernel is taken from:
        - kernel.org

Reference for compilation:
        - https://lukaszgemborowski.github.io/articles/minimalistic-linux-system-on-qemu-arm.html

Taken the source code from https://www.busybox.net/
        - /home/praveenv/sambashare/workspace/BD_new/busybox-1.35.0

reference of compilation and building procedure is taken from
        - https://lukaszgemborowski.github.io/articles/minimalistic-linux-system-on-qemu-arm.html

compiled the busybox and given the command:
        Kernel:
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- versatile_defconfig
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-

        Busybox:
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- defconfig
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- menuconfig
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
                - make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- install
                - mkdir rootfs
                - cd rootfs/
                - ls
                - vim init
                - cd ..
                - chmod +x rootfs/init
                - cp -av _install/* rootfs/
                - mkdir -pv rootfs/{bin,sbin,etc,proc,sys,usr/{bin,sbin}}
                - cd rootfs
                - find . -print0 | cpio --null -ov --format=newc | gzip -9 > ../rootfs.cpio.gz



Run below command for qemu arm:
         qemu-system-arm -M versatilepb -nographic -bios u-boot.bin -kernel ../../linux.git/arch/arm/boot/zImage -dtb ../../linux.git/arch/arm/boot/dts/versatile-pb.dtb -initrd rootfs.cpio.gz -nographic -display none -append "root=/dev/mem"

https://www.codingame.com/playgrounds/84444/running-u-boot-linux-kernel-in-qemu/preparing-bootable-linux-kernel-storage-media
virtual disk:
qemu-system-arm -machine virt -nographic -bios u-boot.bin -device usb-ehci,id=ehci -blockdev driver=file,filename=./disk.img,node-name=disk -device virtio-blk-device,drive=disk
