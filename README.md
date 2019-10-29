# platform-nanopi

nanopi A64 (WIP)  
================

- 20171125 Initial
- u-boot from http://github.com/avafinger/nanopi-a64-firmware  
- dtb from http://github.com/avafinger/nanopi-a64-firmware
- kernel from http://github.com/longsleep/linux-pine64

Unfortunately this u-boot version will only load from an ext4 partition.
Volumio requires the boot partition to be FAT formatted.
To make it work, the default u-boot envornment needed 2 little changes:  

When u-boot fails, it will drop into a boot prompt.  
Issue the next 3 commands:  

- setenv load_bootenv fatload mmc 0:1 ${load_addr} ${bootenv_filename}
- setenv load_bootscript fatload mmc 0:1 ${load_addr} ${script}
- saveenv

The 'saveenv' will write the modified environment to the boot partition as a file 'u-boot.env'
This file will be read in all following boots and can safely be copied to the boot partition when creating images.

Nanopi Neo
=================
- Toolchain gcc version 4.9.3 (ctng-1.21.0-229g-FA)  
- Link to nikkov's work  
https://github.com/nikkov/Volumio-NanoPi-Neo

  
Nanopi Neo2
=================

- 20191029 Initial

- Toolchain gcc version 6.3.1 20170109 (Linaro GCC 6.3-2017.02)
- u-boot from https://github.com/friendlyarm/u-boot.git   
branch: sunxi-v2017.x 
- kernel from https://github.com/friendlyarm/linux.git  
branch sunxi-4.14.y
- dtb modifications
enable pcm5101a
enable i2s0
disable i2c1 & i2s2
- kernel modification "sound/soc/codecs/Kconfig"
locate "config SND_SOC_PCM5102A"
then modify 'tristate' to 'tristate "Texas Instruments PCM5102A"'

- 20191029/ gkkpch  
patch for improved ALSA DSD direct support  




