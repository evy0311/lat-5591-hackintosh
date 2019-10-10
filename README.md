# Dell Latitude 5591 - Hackintosh Guide

### Overview

- This guide references a few other guides. Credit for those guides is given to their respective owners.
- It is assumed that you have a decent understanding of Hackintosh, the macOS environment, as well as how to do basic computer tasks
- Will guide you through some of the different information needed to get macOS Mojave 10.14.6 working on your Dell Latitude 5591.
- Special thanks to n0faith and his repo [Here](https://github.com/n0faith/Dell-Precision-5591-Hackintosh "Here") for providing kexts and other configuration info, as well as the patched ACPI files. Also a special thanks to [midi1996](https://github.com/midi1996) on GitHub for his guide on how to create the macOS installer from Recovery.
- **Note:** I am NOT responsible for any harm you cause to your device. This guide is provided "as-is" and all steps taken are done at your own risk

# Guide

<img src="https://github.com/evy0311/lat-5591-hackintosh/raw/master/Guide%20Stuff/5591-mojave.png" width="50%" height="50%">

![](https://img.shields.io/github/issues/evy0311/lat-5591-hackintosh) ![](https://img.shields.io/github/forks/evy0311/lat-5591-hackintosh) ![](https://img.shields.io/github/stars/evy0311/lat-5591-hackintosh) ![](https://img.shields.io/github/license/evy0311/lat-5591-hackintosh) ![](https://img.shields.io/twitter/url?url=https%3A%2F%2Fgithub.com%2Fevy0311%2Flat-5591-hackintosh)


## Information
##### What works:
- Power management/sleep
- Brightness Control
- Battery Information
- Audio (from internal speaker and headphone jack)
- USB Ports
- Graphics Acceleration
- Facetime/iMessage
- Touchpad (with all gestures)
- WiFi and Bluetooth (with Broadcom WiFi/Bluetooth card)
- Dell D3100 USB 3.0 Dock (all ports)

## More Information
The laptop I am specifically using is the Dell Latitude 5591 with the follows specsifications.
##### Specs:
- Model: Dell Latitude 5591
- BIOS: 1.11.0
- CPU: Intel® Core™ i7-8850H (6 Core - 12 Thread) ~ 2.6 - 4.3Ghz
- GPU: Intel UHD630 1536MB
- RAM: 2 x 2667MHz Samsung 16GB Single Channel LPDDR4
- Display: 15.6 inch 16:9, 1920 x 1080 pixel 141 PPI
- Storage: NVME PCIE 3.0 x4 Toshiba XG5 KXG50ZNV512G 512 GB
- LAN: Intel Ethernet Connection I219-LM (10/100/1000/2500/5000MBit/s)
- Wireless: DW1560
- Bootloader: Clover v2.5k r5093

Your mileage may vary when installing macOS on your 5591, since these units could be configured with many different options from the factory. Thankfully, the general configuration is mostly the same. If you have any questions regarding your specific case or need help in general, feel free to contact me via email at <evy0311@gmail.com>.

## Creating the USB Installer
Since I don't have access to a legitimate Mac, I needed to be able to create a vanilla macOS installer. This guide (and many others) used to inform users to create a USB installer for a macOS Distro such as Niresh. While this may work just fine for then creating a vanilla macOS installer, distro's can be (and are) very shady. They come preloaded with a bunch of extra junk that is not needed, and just overall are *highly* advised against being used. Follow the steps below to figure out how to create a REAL macOS Mojave Vanilla installer without having access to a real Mac.

1. Follow the steps at this guide [Here](https://internet-install.gitbook.io/macos-internet-install/).
2. When you get to the part about installing clover bootloader, follow the steps below for configuring kexts, etc. 
3. **IMPORTANT (DO NOT MISS THIS):** Now, copy Clover bootloader and the kexts files that you have downloaded to another USB drive (not the one you're burning the installer too) or an external hard drive. You will need access to them later.
4. Copy the `CLOVER` folder you have downloaded from this repository onto your USB drive as well.
5. Copy the `CLOVER` folder you have downloaded from this repository into `EFI/`. You can simply copy over the whole folder as the config.plist and everything else is already configured for the T440p. 
6. The most important step that I missed twice in the guide above is to make sure you add the `HFSPlus.efi` driver into `/EFI/Clover/drivers64UEFI`. I missed this step twice and couldn't see any drivers at all inside of Clover.
7. For more help on configuring Clover and the USB installer, the original guide linked in step 1 will be of the most help to you. Make sure you install the kexts and `CLOVER` folder from this repo onto your Clover USB, as these will guarantee your T440p will work properly.
8. We are now ready to continue into the next topic: Installing macOS Mojave.



## Installing macOS Mojave
1. After you followed the guide above and have your USB drive ready to go, we can reboot the machine. When you reboot, enter into the BIOS to change some settings. On the T440p, you can do this by hitting `Enter` at the Lenovo boot screen.
2. Once in the BIOS, make sure you change the following settings. `Disable Security Chip`, `Disable Anti Theft Module`, and `Disable TPM`. Basically, disable all of the "security" features. Make sure Secure boot and other features like that are off. These features will affect how macOS sleeps.
3. Now, reboot into macOS and select the USB drive inside of Clover.
4. Boot into macOS and install onto your hard drive. I recommend using an SSD.
5. After this is done, reboot the computer and let it sit. Mine rebooted a few times on its own to go through some final installation procedures.
6. Once you see the "region selection" screen, you are good to proceed.
7. Create your user account and everything else, but do not sign in with your iCloud account. If it asks you to connect to a network, select the option that says do not connect and press continue. We will connect it later.
8. After you've booted, plug in the USB drive or external hard drive that you copied the Clover file to in step 9 of the previous section. 
9. Install Clover bootloader following the same steps as before and using the same settings, except this time install them onto your internal hard drive with your Mojave installation. I recommend checking the box that says `Install Clover Configurator` as well (it comes in handy later).
10. We now need to copy our Clover configuration from our USB to our hard drive with Mojave. Simply copy the `CLOVER` folder that you have on your other USB drive (the one you used in step 9 of the previous section) into the `EFI` partition that Clover should have mounted during install. 

## Post-Installation

##### Setting up Apple services (Facetime, iMessage, etc.)
I *highly* recommend following [This guide](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/) to get these features working. It worked for me on the first try and was super straight forward compared to other guides that I have seen before in the past. 

##### Customizing About This Mac

In order to customize the About This Mac section, I recommend you follow the guide [Here](https://github.com/Haru-tan/Hackintosh-Things/blob/master/AboutThisMacMojave.md "Here").

For the section about changing the logo, you can use the T440p logo's I have designed in ` /SystemLogos/`.