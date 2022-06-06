# fx3fun

[![Cypress FX3 as a Possible Logic Analyzer](https://img.youtube.com/vi/_LnZrXrdC00/0.jpg)](https://www.youtube.com/watch?v=_LnZrXrdC00)

I'm trying to turn the Cypress FX3 into a logic analyzer.  I've been playing with a kit, specifically the $45 http://www.cypress.com/documentation/development-kitsboards/cyusb3kit-003-ez-usb-fx3-superspeed-explorer-kit - and I've found it to be incredibly powerful.  This project is split up into a few components.

1. The Firmware: It is firmware that turns the GPIF-II bus into a 16-bit, 100 MHz sampling device.  Synchronously receiving data and storing it in a buffer to stream back to a computer.  My firmware sets up the isochronous pipes in such a way to transfer data back at about 250 MB/s.  Also, control messages are really easy to send, so this could also be a really useful tool for programming chips, too!  Currently, I'm still using the Windows tools to compile, but shouldn't be hard to use GCC ARM to compile in Linux, especially with the Official Cypress SDK.

2. CyprIO (pronounced saɪˈpirˈēˈō): My C-library for use in Windows (with CyUSB32.sys) or Linux (with libusb) that lets you talk to my firmware on the cpress chip. 
Originally Cypress offered a CyAPI that let you use C++ to talk to their parts, but in digging into it, I found that it was extremely overbearing, and just not a 
good fit for many of the projects I wanted (see Sigrok support below). So, I re-wrote it, in C. 

Also, a side benefit of this is you can compile it and use it in Windows with only TCC (a 6MB package). All header files needed to compile are included.  No Visual Studio needed or anything.

The PC-side software works in Windows (TCC) or Linux (GCC). Test in both as of Dec 31, 2017. Who knows if it'll keep working.

3. isotest - make control transfer to start sampling GPIF bus and receives data coming back. (Uses CyprIO)

4. cyprflash - tool that uses CyprIO to boot images on the FX3, and potentially flash a tool that allows writing to an I2C EEPROM on-board, using the official cypress flasher firmware.  NOTE: Shouldn't be hard to support an SPI EEPROM, but I don't have a board with SPI EEPROM to test against.

# Sigrok support

Here are some experiments and ongoing progress as of June 2022:

1. [libsigrok-cypress-fx3-test](https://github.com/schnommus/libsigrok-cypress-fx3-test)
1. [libsigrok pullrequest](https://github.com/sigrokproject/libsigrok/pull/148)

# Brief installation notes.

 * `git clone https://github.com/cnlohr/fx3fun`
 * Register and download the Cypress EZ-USB FX3 SDK for your OS [here](https://www.infineon.com/cms/en/design-support/tools/sdk/usb-controllers-sdk/ez-usb-fx3-software-development-kit/)
 * You will find "fx3_firmware_linux.tar.gz" and you can take that and drop "cyfx3sdk" in the same folder that "fx3fun" is located in, so they are parallel.
 * Make a folder in your home folder called `Cypress`
 * Unzip, from the SDK the following folders into `Cypress`
   * `arm-2013.11`
   * `cyusb_linux_1.0.5`

Add the following to your `.bashrc` or `.zshrc`, YMMV:

```
export PATH=$PATH:$HOME/Cypress/arm-2013.11/bin
export FX3_INSTALL_PATH=$HOME/Cypress/cyfx3sdk
export ARMGCC_INSTALL_PATH=$HOME/Cypress/arm-2013.11
export ARMGCC_VERSION=4.8.1
export CYUSB_ROOT=$HOME/Cypress/cyusb_linux_1.0.4

Then operate the different tests and fun as follows:

```
 * `. ~/.bashrc`
 * Optional if you want to build the firmware:
   * `cd fx3fun/testproject/USBIsoSource`
   * `make`
   * cp ?????? TODO: How to do firmware? BIG TODO: No, really how do you actually make the firmware?  
   * On Windows it looks like it uses `elf2img.exe`
   * `cd ../../`
 * `cd cyprflash`
 * `make`
 * Hold the PMODE jumper shorted.
 * `sudo ./cyprflash  -i -f streaming_image.img`
 * `cd ..`
 * Reboot board, make sure it's up:
   * `lsusb -vv -d 04b4:00f1`
 * ISO Test
   * `cd isotest`
   * 
```

Happy high speed hacking!
