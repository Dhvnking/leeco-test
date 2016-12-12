LeEco Le 2 (s2) Kernel Build Guide     
===============================



The LeEco Le 2 (Indian Version Codenamed "s2") is a smartphone from LeEco or LeMobile Information Technology Co. Ltd.



Device configuration for s2
=====================================

Basic   | Spec Sheet
-------:|:-------------------------
CHIPSET | Qualcomm MSM8976 Snapdragon 652
CPU     | Quad-core 1.4 GHz Cortex-A53 & Quad-core 1.8 GHz Cortex-A72
GPU     | Adreno 510
Memory/RAM  | 3 GB
Storage | 32 GB
Battery | 3000 mAh (Non-Removable)
Dimensions | 151.1 x 74.2 x 7.5 mm
Display | 1080 x 1920 pixels 5.5"
Rear Camera  | 16.0 MP
Front Camera | 8.0 MP
Release Date | June 2016



![LeEco Le 2](http://in.img3.lemall.com/file/20160606/default/3370481864506311 "LeEco Le 2")



# Download, Prepare and Compile the Kernel
--------


- Download Toolchains (CAF Toolchains Used Below. Other Toolchains may Cause Problems.)


		$ git clone https://source.codeaurora.org/quic/la/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 -b LA.BR.1.3.5.c1_rb1.3



- Download Kernel Sources


		$ git clone https://github.com/s2-devs/android_kernel_leeco_msm8976.git -b stock-6.0



- Change Directory to Kernel Directory and Make Output Folder


		$ cd android_kernel_leeco_msm8976


		$ mkdir out



- Prepare Source for Compilation


		$ export CROSS_COMPILE=../aarch64-linux-android-4.9/bin/aarch64-linux-android-


		$ export ARCH=arm64;



	Now set how many files to compile at once. This number could be "The Number of Cores in your PC's Processor + 2"


		$ export JOBS=8



- Clean Sources for Building and for Rebuilding


		$ make clean


		$ rm -fdr out


		$ mkdir out



- Compile the Kernel and Sign the WiFi Module to Fix WiFi Error


		$ make s2-perf_defconfig


		$ make -j$JOBS


		$ make -j$JOBS KCFLAGS=-mno-android


		$ make -j$JOBS KCFLAGS=-mno-android modules


		$ scripts/sign_file.sh sha512 ./sign_key.priv ./sign_key.x509 ./drivers/staging/prima/wlan.ko



# 2. Get Compiled Kernel Output
---------------


- Kernel: out/arch/arm64/boot/Image.gz-dtb

- Kernel modules: out/drivers/*/*.ko



# 3. Doubts?
---------------


#### IF YOU WANT THE COMPLETE KERNEL BUILD GUIDE FOR THIS DEVICE, THEN PLEASE CHECK OUT THIS XDA POST: [[Guide]Compiling WORKING 64 bit Android Kernel [Le2] [NOOB Friendly]](http://forum.xda-developers.com/le-2/how-to/guide-compiling-64-bit-android-kernel-t3512749)



# Credits
--------


- Bhavya Singhal [Brawn_Sg](http://forum.xda-developers.com/member.php?u=5938667)
- [Rishabh Rao](http://forum.xda-developers.com/member.php?u=5890172)
- [13THWARRIOR](http://forum.xda-developers.com/member.php?u=5708300)
- Lakshay Taneja [Lakku](http://forum.xda-developers.com/member.php?u=6735776)
- Jignesh Jain [jhakjhuk1853](http://forum.xda-developers.com/member.php?u=4978710)




