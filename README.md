# candleLight_gsusb

This is a firmware for stm32f0-based USB-CAN adapters, notably:
- candleLight: https://github.com/HubertD/candleLight
- cantact: http://linklayer.github.io/cantact/
- canable (cantact clone): http://canable.io/
- USB2CAN: https://github.com/roboterclubaachen/usb2can

It implements the interface of the mainline linux gs_usb kernel module and 
works out-of-the-box with linux distros packaging this module, e.g. Ubuntu.

Be aware that there is a bug in the gs_usb module in linux<4.5 that can crash the kernel on device removal.

Here is a fixed version that should also work for older kernels:
  https://github.com/HubertD/socketcan_gs_usb

The Firmware also implements WCID USB descriptors and thus can be used on recent Windows versions without installing a driver.

## To Flash a Canable board on Linux
1) Install dfu-util ```sudo apt install dfu-util```
2) Press the boot button on the Canable board while plugging in the micro usb
3) Release the boot button
4) Navigate to the bin directory of this repo
4) Run ```sudo dfu-util -d 0483:df11 -c 1 -i 0 -a 0 -s 0x08000000 -D gsusb_canable.bin```

## To compile firmware for a Canable board on Linux
Requirements: arm-none-eabi-gcc - ```sudo apt-get install gcc-arm-none-eabi```
1) Navigate to the root directory of this repository
2) Run ```make BOARD=canable```
3) This will generate multiple bin files. The file needed for the canable device is ```gsusb_canable.bin``` shown above
