---
layout: post
title: Jailbreak a Nixplay W10P Photo Frame
cover: /assets/img/cover-hack.jpg
tags:
- software
- walkthrough
---

I own an older Nixplay W10P frame from 2023 which, despite having gigabytes of
free space, will no longer accept new photos due to recent [mandatory changes
in the Nixplay's terms of
service](https://www.nixplay.ca/blogs/legal-policy-documents/important-update-from-nixplay-ceo-2025-changes-to-your-services-a).
I'm not opposed to a company charging for services but their reasoning of
"rising storage and bandwidth costs" is unconvincing given both have declined
significantly in recent years.  It's reasonable to speculate that the next
update will continue to erode the reasons I chose the frame in the first place.
Who wants to bet it will be something to do with AI?

Anyway, I've decided to decline these new terms and delete my Nixplay account.
However, I don't want to lose the functionality of the hardware.  Yo-less
uploaded a detailed [video on youtube demonstrating how to jailbreak the
Nixplay frame](https://www.youtube.com/watch?v=TN5errM5UbA).  The process
seemed straightforward, involving nothing more than plugging a cord into a W10E
frame and connecting to `adbd`.  I found that the process for the older W10P
model was not as seamless. Since I spent a chunk my weekend working through
this, I wanted to document the steps here to help others who may face similar
issues.

<hr />

**The good news:** You don't have to take your frame apart at all.  Both the
USB port and the reset button are accessible externally.

**The bad news:** Unfortunately, the firmware does not include the `adbd`
executable in the system image, so it’s not immediately possible to connect to
the frame using `adb`. I am using macOS for this process, and when first
plugging in the frame, it does not show up in the system by default:

```bash
% brew install usbutils
% lsusb
Bus 000 Device 001: ID 1d6b:XHCI
XHCI
XHCI Linux Foundation USB 3.1 Bus
```

Hold down the reset button for about 5 seconds and try it again though:

```bash
% lsusb
Bus 002 Device 001: ID 2207:310d Fuzhou Rockchip Electronics Co., Ltd. Composite Device
Bus 000 Device 000: ID 2207:310d Fuzhou Rockchip Electronics Co., Ltd. USB 3.1 Bus
Bus 000 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
```

It lives!  At this point, the frame is detected. The screen will go black, and
Android tools will not yet be functional, but we can use this bootloader to
proceed. Let's start by getting the necessary tools.

```bash
# brew's rkflashtool.  Note the syntax is slightly different than linux's...
brew install rkflashtool
# adb & friends
brew install --cask android-platform-tools
```

I suggest taking a full backup just in case but we actually only need the
system and recovery images.  Skip the `userdata.img` at the end unless you have
a specific need as it takes a couple of hours to run.

```bash
#!/bin/bash

# Script courtesy of ChatGPT.  Note that if you don't have a `W10P` model frame these offsets might not be right!

# Make sure rkflashtool is in your PATH or use full path
RKFLASHTOOL=rkflashtool

echo "Dumping uboot..."
$RKFLASHTOOL r 0x00002000 0x00002000 > uboot.img

echo "Dumping trust..."
$RKFLASHTOOL r 0x00004000 0x00002000 > trust.img

echo "Dumping misc..."
$RKFLASHTOOL r 0x00006000 0x00002000 > misc.img

echo "Dumping resource..."
$RKFLASHTOOL r 0x00008000 0x00008000 > resource.img

echo "Dumping kernel..."
$RKFLASHTOOL r 0x00010000 0x00006000 > kernel.img

echo "Dumping boot..."
$RKFLASHTOOL r 0x00016000 0x00006000 > boot.img

echo "Dumping recovery..."
$RKFLASHTOOL r 0x0001C000 0x00010000 > recovery.img

echo "Dumping backup..."
$RKFLASHTOOL r 0x0002C000 0x000A0000 > backup.img

echo "Dumping cache..."
$RKFLASHTOOL r 0x000CC000 0x000A0000 > cache.img

echo "Dumping metadata..."
$RKFLASHTOOL r 0x0016C000 0x00008000 > metadata.img

echo "Dumping kpanic..."
$RKFLASHTOOL r 0x00174000 0x00002000 > kpanic.img

echo "Dumping radical_update..."
$RKFLASHTOOL r 0x00176000 0x00020000 > radical_update.img

echo "Dumping keys..."
$RKFLASHTOOL r 0x00196000 0x00008000 > keys.img

echo "Dumping system..."
$RKFLASHTOOL r 0x0019E000 0x00280000 > system.img

echo "Dumping userdata (rest of flash)..."
# adjust length if you know exact remaining size
$RKFLASHTOOL r 0x0041E000 0x00C00000 > userdata.img

echo "All partitions dumped."

```

The next step is to add the `adbd` executable, which is missing from the system
image. Fortunately, it exists in the recovery image.  I had to use Debian to
manage all the image modification because I didn't want to fight OS X and ext4.
Here’s how to extract it.

```bash
# on debian
mkdir recovery_wd
cd recovery_wd
cp ../recovery.img .
# creates zImage, initrd.img, and bootimg.cfg.
# `apt install abootimg` if you need to
abootimg -x recovery.img
mkdir ramdisk
cd ramdisk
gzip -dc ../initrd.img | cpio -i

# You'll find a copy of `adbd` in /sbin/ but first we'll need to mount the system image so we have a place to put it.

cd ../..
mkdir simg
mount -t ext4 system.img simg
cd simg
# Now you're in the system image we dumped from the frame
mkdir sbin
cd sbin
cp ../../recovery_wd/ramdisk/sbin/adbd .
chmod 755 adbd
cd ../..
sync
umount simg
```

Now that the system image includes `adbd`, it's time to write it back to the frame.
```bash
# Write to the system partition
rkflashtool w system < /path/to/system.img
# Reboot
rkflashtool b
```

At this point `adbd` is present but not auto-starting. There are multiple
conditions in the system's `init.rc` file to start `adbd` (e.g. `on
property:sys.usb.config=adb && property:sys.usb.configfs=1`) and presumably one
of those doesn't get set.  I didn't want to keep chasing this so next we'll
patch the boot image to just start adbd directly:

```bash
# back on debian
mkdir bood_wd
cd boot_wd
cp ../boot.img .
abootimg -x boot.img
mkdir ramdisk
cd ramdisk
gzip -dc ../initrd.img | cpio -i
```

Add these lines within the existing `on boot` section of the `init.rc` above
the `class_start default` line.
```
    setprop sys.usb.config adb
    setprop sys.usb.configfs 1
    setprop service.adb.root 1
    start adbd

    write /sys/class/android_usb/android0/enable 0
    write /sys/class/android_usb/android0/idVendor 18D1
    write /sys/class/android_usb/android0/idProduct D001
    write /sys/class/android_usb/android0/functions adb
    write /sys/class/android_usb/android0/enable 1
```

And then create a new boot image with this change:
```bash
find . | cpio -o -H newc | gzip > ../initrd-new.img
cd ..
abootimg --create ../boot-new.img -f bootimg.cfg -k zImage -r initrd-new.img
```

Transfer the new image to the frame
```bash
rkflashtool w boot < boot-new.img
rkflashtool b
```

After rebooting the frame `adbd` should fire up.  `adb` commands (and `vysor`
from the original video) should be able to connect and you can follow the
directions in the video to install the apps you want.
