# ZTE Open B2G update procedure for OSX #

Thanks to Eduardo González for the source linux [tutorial](http://sl.edujose.org/2013/09/zte-open-hack-actualizando-fxos-11.html) ;-) 

## Download tools.zip

	Decompress and open shell location

## Root your phone

[ZTE OPEN Root Post](http://pof.eslack.org/2013/07/05/zte-open-firefoxos-phone-root-and-first-impressions/)

	./root.sh

## Backup your existing recovery

**Remember to disable USB Storage while doing this**
	
	adb shell
	su
	dd if=/dev/mtd/mtd0 of=/sdcard/stock-recovery.img bs=4k

**Save your original recovery**
	
	adb pull /sdcard/stock-recovery.img
	
## Flash clockworkmod recovery

	adb push recovery-clockwork-6.0.3.3-roamer2.img /sdcard/cwm.img
	adb shell
	su
	flash_image recovery /sdcard/cwm.img

**Restart Phone!!**

## Extract boot.img to sd card

	adb shell
	su
	cat /dev/mtd/mtd1 > /sdcard/boot.img

## Apply boot.img patch

	./patch.sh
	
## Restart phone in CWM recovery mode ( power + volume up )

Enter phone with:

	adb shell
	su
	mount /sdcard
	flash_image boot /sdcard/patchedBoot.img	
		

## Flash B2G

Goto to your B2G dir and type:

	./flash.sh gaia
	./flash.sh gecko

## Reboot

If phone don't wake up go to your B2G dir and type:

	cd gaia
	make reset-gaia