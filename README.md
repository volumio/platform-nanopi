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

**20191029/ gkkpch**

- patch for improved ALSA DSD direct support

**20191030/ gkkpch**

- reverted to kernel 4.11.y (4.11.2+)
- added nikkov's dtb's
- default dtb copied to "sun50i-h5-nanopi-neo2.dtb":
  *sun50i-h5-nanopi-neo2-i2s-generic.dtb*
- fixed an issue with mmc, reverted the following patch
https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/drivers?id=2154d94b40ea2a5de05245521371d0461bb0d669

**20191029/ gkkpch**
- Kernel: removed support for formats >192Khz
- Kernel: created default neo2 dts and neo2-i2s-generic dts from nikkov's dtb

**20210301/ gkkpch**
- Kernel: switched to nikkov's friendlyarm 4.14, taken from MINIDSP
- Kernel: added sun4i-i2s patch for swapping L/R channels, taken patch from MINIDSP
- boot.cmd modified version to run with 4.14, taken from MINIDSP
- Modified kernel params to include cp15 barrier emulation

Nanopi Neo3
=================

- kernel from https://github.com/friendlyarm/kernel-rockchip
- branch: **nanopi-r2-v5.4.y**
- u-boot from Armbian package **linux-u-boot-current-nanopineo3_20.08.0-trunk_arm64.deb**
- dts based on **rk3328-nanopi-r2-rev00.dts** with
   added pcm5102a codec node
   added sound-i2s node
   enabled i2s
- pinctrl for i2s fixed by removing conflicting pins from leds_gpio

 **20200907/ gkkpch**
 - Initial platform files for NanoPi Neo3
 - Change dtb name to rk3328-nanopi-neo3-rev02.dtb
 - Change USB mass storage to kernel built-in module

 **20201203/ gkkpch**
 - Updated WiFi settings, added latest Realtek & Ralink firmware

**20201209/ gkkpch**
- Updated Realtek/Ralink firmware

**20201221/ gkkpch**
- Limited audio to 16 and 24bit









