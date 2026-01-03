# Getting the latest rpi-imager

When I tested some older `rpi-imager` releases (prior to 2.0), they did get a bootable image of Trixie onto an SD card.  
But they didn't actually *configure* the image (so creating an SD card for a headless PI was unsuccessful.)  
Luckily, they did get Trixie onto the SD card, unconfigured, and it would boot on a PI with a keyboard & display such that it could be 
manually configured by filling out the menu prompts that will appear during the first boot.

Alternately, you can use any Unix(ish) box to manually copy a Raspberry PI OS desktop image onto an SD card without the rpi-imager at all.

Running a desktop on a PI can *then* be used to run the latest `rpi-imager` *and* configure an SD card for use on a headless system!

# Burning an SD card (without rpi-imager) to boot a desktop on a PI

**WARNING** Doing this incorrectly can instantly, unrecoverably, destroy the filesystem on the machine you are using. Do not do this if you don't understand the process!!!!! **DO NOT blindly copy these commands expecting everything will be OK.**

Download the latest OS image from raspberrypi.com.  The one I used while writing these notes is:

	wget https://downloads.raspberrypi.com/raspios_arm64/images/raspios_arm64-2025-12-04/2025-12-04-raspios-trixie-arm64.img.xz

Insert the SD card you want to image and identify the device name.  Depending on the SD card adapter you are using and the configuration of your machine, it can be any one of a number of places.  This is the critical thing to get right.  Consider using commands like `lsblk` to locate the SD card, then remove the SD card, run `lsblk` again, note that it has gone away, and then finally returns when it is plugged back in... for an absolute positive confirmation of the SD card's device name.

If your machine mounts whatever existing junk might be on your SD card, you will want to unmount it like this:

	sudo umount /dev/sdXXXX

I then wipe and program the SD card like this (on my system, the SD card is `/dev/sdb`):

	SD=/dev/sdb
	sudo dd if=/dev/zero of=$SD bs=4M count=1 status=progress conv=fsync
	sudo xzcat 2025-12-04-raspios-trixie-arm64.img.xz | dd of=$SD bs=4M status=progress conv=fsync
	sync

At this point you have a bootable Trixie SD card with a full desktop that is unconfigured.  It can boot on a PI with a keyboard and display.  It will boot into a configuration menu to create a user account, set the timezone and so on.  After that, it can be used to run the latest `rpi-imager` to create an SD card that can boot on a headless PI.
