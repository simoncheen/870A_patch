# 上传文件，分别打patch #


# 配置变量环境 #
```bash
./build.sh EM3288_870A_debian.mk
```

# 编译uboot #
```bash
cd u-boot
./make.sh EM3288_870A
```

# 编译kernel #
```bash
cd ../kernel/
make ARCH=arm EM3288_870A_defconfig 
make ARCH=arm menuconfig
make ARCH=arm EM3288_870A.img -j8
make -j8 ARCH=arm modules
```

# 编译recovery(可以忽略) #
```bash
cd ..
./build.sh recovery
```

# 编译rootfs #
```bash
cd rootfs
ARCH=armhf ./mk-base-debian.sh
RELEASE=stretch ARCH=armhf ./mk-rootfs.sh
./mk-image.sh
```

# 导出所有img #
```bash
cd ..
./mkfirmware.sh
```

========================================
# notice: #
单独输出linux-boot.img (带ramdisk)
```bash
mkbootimg --kernel kernel/arch/arm/boot/zImage --ramdisk initrd.img --second kernel/resource.img  -o linux-boot.img
```


## 可能导致I2C timeout ##
```
FIQ
```