# usb-lan
FIXs problem usb lan 0fe6:9702 openwrt

Leave the adapter unplugged. First, we made a backup of the driver.
* cd /lib/modules/5.15.120-ophub/
* cp dm9601.ko dm9601.ko.orig

Next, we modify the driver:
* opkg install xxd
* xxd dm9601.ko | sed 's/e60f 0097/e60f 0297/g' | xxd -r > dm9601.ko.mod

Then, we strip it.
* opkg install binutils
* strip --strip-debug dm9601.ko.mod

Then we copy the modified driver
* cp dm9601.ko.mod dm9601.ko

Last, we load the modified kernel module
* modprobe -r dm9601 && modprobe dm9601
* reboot

  Now, this is important, plug the Ethernet in BEFORE plugging in the USB. 
If you don't, it won't work. 

cek on webui network device
