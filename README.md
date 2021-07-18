I've slightly modified the guide to be specifically for this router.

For convenience, wifi is enabled by default on first boot. If you do not want this, remove ``./target/linux/ramips/base-files/etc/uci-defaults/99_wireless_config``

Special thanks to [sanitariu](https://forum.openwrt.org/t/support-for-tl-wr840n-ver-6-0/17041/113) & [milankragujevic](https://github.com/milankragujevic/openwrt-wr840n-v620-old/blob/master/target/linux/ramips/dts/mt7628an_tplink_tl-wr840n-v6.dts) for the source files and guides!

```
  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------

This is the buildsystem for the OpenWrt Linux distribution.

To build your own firmware you need a Linux, BSD or MacOSX system (case
sensitive filesystem required). Cygwin is unsupported because of the lack
of a case sensitive file system.

You need gcc, binutils, bzip2, flex, python, perl, make, find, grep, diff,
unzip, gawk, getopt, subversion, libz-dev and libc headers installed.

1. Run "./scripts/feeds update -a" to obtain all the latest package definitions
defined in feeds.conf / feeds.conf.default

2. Run "./scripts/feeds install -a" to install symlinks for all obtained
packages into package/feeds/

3. Run "make menuconfig" to select your preferred configuration for the
toolchain, target system & firmware packages.

3.1. With the config menu open, select these:
  Target System:  MediaTek Ralink MIPS
  Subtarget:      MT76x8 based boards
  Target Profile: TP-Link TL-WR840n v6.2

3.2. (Optional) Change to fit new features:
 + Enable (built-in)     - Disable

 Target Images > squashfs:
   + Block size: 512 (1024 if bin is still big, slower boot time)

 Global build settings:
   - Cryptographically signed package lists
   - Enable signature checking in opkg
   + Remove ipkg/opkg status data files in final images
   - Enable IPv6 support in packages
   + Strip unnecessary exports from the kernel image
   + Strip unnecessary functions from libraries
   Kernel build options:
     - Compile the kernel with debug filesystem 
       (disable mac80211 DebugFS first)
     - Compile the kernel with symbol table info
     - Compile the kernel with debug info
     + Number of squashfs fragments cached: 1
     + Compiler optimination level: Optimize for size

 Base system:
   - opkg
   - openwrt-keyring
   - libpthread

 Network:
   - ppp

 Kernel modules:
   Wireless Drivers > kmod-mac80211:
     - Export mac80211 internals in DebugFS
   Network support:
     - kmod-ppp

 LuCI:
   Modules:
     + luci-base
     + Minify Lua sources
   Themes:
     + luci-theme-bootstrap

Read more in https://openwrt.org/docs/guide-user/additional-software/saving_space

4. Run "make" to build your firmware. This will download all sources, build
the cross-compile toolchain and then cross-compile the Linux kernel & all
chosen applications for your target system.

.bin files are located in ./bin/targets/ramips/mt76x8
If your sysupgrade bin goes over 3.5MB, there will not be enough
space for jffs2 to save. It'll boot, but settings won't persist
between reboots.

Sunshine!
    Your OpenWrt Community
    http://www.openwrt.org

    IcedShake
    https://github.com/IcedShake
```
