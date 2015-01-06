## chrubuntu-script

This is a script to install ChrUbuntu on a Chromebook. This is effectively a fork of the script that is described and referenced at [http://chromeos-cr48.blogspot.co.uk/2013/05/chrubuntu-one-script-to-rule-them-all_31.html](http://chromeos-cr48.blogspot.co.uk/2013/05/chrubuntu-one-script-to-rule-them-all_31.html). This repo contains a modified version of the file located at [http://goo.gl/s9ryd](http://goo.gl/s9ryd).

###  Notes/Motivation for this version:
* All credit goes to [Jay Lee](https://plus.google.com/+JayLee/posts) and his [Chromebooks and Chrome OS blog](http://chromeos-cr48.blogspot.co.uk/).
* While there is a ton of information on Jay's blog, I found it confusing to not have a proper source repository for the code and documentation so I have organized my notes into this repository.
* It appears that `parted` [was removed from ChromeOS at some point](https://github.com/omgmog/archarm-usb-hp-chromebook-11/issues/14), so the original script no longer worked for me. I stumbled across some useful information on the [Arch Linux ARM Samsung Chromebook](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook) page that used `partx` instead. This proved to work for this script as well.
* I have only tested this on a [Samsung Chromebook 2](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/samsung-chromebook-2) since this is the only hardware I have access to.

## Usage
With your Chromebook in developer mode, press `CTRL+ALT+=>` at the main login screen (=> is the forward arrow where the F2 key would be on a PC). Log in with the username `chronos`.

At the prompt, enter a command in the following form:

    curl -L -O https://raw.githubusercontent.com/jalessio/chrubuntu-script/master/chrubuntu-install.sh
    sudo bash chrubuntu-install.sh [flavor] [version] [target-disk]

#### Versions:
* lts -- latest LTS Ubuntu release, 14.04 as of this writing
* latest -- latest official release, currently 14.10
* dev -- unstable development Ubuntu release, experts only! If this breaks, don't be surprised
* 12.04.5 -- Ubuntu 12.04.5 release

#### Flavors:
* default  (ubuntu-desktop on x86, xubuntu-desktop on arm)
* kubuntu-desktop
* lubuntu-desktop
* xubuntu-desktop
* edubuntu-desktop
* ubuntu-standard (no GUI installed)

#### Examples:
Samples I have run successfully on a [Samsung Chromebook 2](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/samsung-chromebook-2):

    sudo bash chrubuntu-install.sh ubuntu-standard 12.04.5 /dev/mmcblk1
    sudo bash chrubuntu-install.sh ubuntu-standard 14.04 /dev/mmcblk1

### Toggle booting between Chrome OS and ChrUbuntu:
I have placed to helper scripts on the system to help with toggling between Chrome OS and ChrUbuntu. The following two commands should be available in your path.

To boot into Chrome OS by default:
    
    sudo boot2chromeos

To boot into ChrUbuntu by default:

    sudo boot2chrubuntu

The full path to the scripts is:

    /usr/local/bin/boot2chromeos
    /usr/local/bin/boot2chrubuntu

---
### Here's a (slightly modified) copy of [original documentation]((http://chromeos-cr48.blogspot.co.uk/2013/05/chrubuntu-one-script-to-rule-them-all_31.html):):

* A single script that works on ALL Chrome devices including the ARM-basedSamsung Chromebook.
* A single script that can install any Ubuntu version: 14.04 LTS, 13.10, 12.04.5, even the latest daily dev image.
* A single script that can install Ubuntu, Kubuntu, Lubuntu, Xubuntu, Edubuntu or many other desktop variants.
* A fully up-to-date ChrUbuntu install on boot. No more downloading hundreds of megabytes in updates after first boot.

### Installation:
1. To get started, make sure your Chromebook is in developer mode and has a developer BIOS installed. See Google's instructions for your model. Older Samsung and Acer owners should pay special attention to the Developer BIOS instructions.

2. Start with your Chrome device turned off. Turn it on but do not login. Make sure you have a WiFi or Ethernet connection configured at this point. 3G/4G is not recommended. Press CTRL+ALT+=> (=> is the forward arrow where the F2 key would be on a PC). Do not use the normal CTRL+ALT+T method to get a shell. Use the CTRL+ALT+=> method while no one is logged in.

3. Login as user chronos, no password is needed.

4. As the chronos user and without having changed directories or run other commands, run:

        curl -L -O https://raw.githubusercontent.com/jalessio/chrubuntu-script/master/chrubuntu-install.sh
        sudo bash chrubuntu-install.sh

    Make sure you have the command exactly right. The -O and -L after curl are both capital letters. If you get a "not found" error, make sure you have Internet connectivity and you're typing the commands correctly.

5. You'll be prompted with some information about your Chromebook. You may need to run an additional command to install a developer BIOS on your Chromebook. Press Enter to continue.

6. The Chrome OS stateful partition where your data and settings are stored is just short of 11gb by default (except for the Acer C7 where it is much larger), the script shrinks the stateful partition to make room for ChrUbuntu. You can choose to give ChrUbuntu from 5gb up to 10gb in 1gb increments (Note: If you've installed a larger SSD in your Chrome device, your max number and recommended max will be larger). I recommend not going higher than 9 as 10 leaves Chrome OS with very little free space (less than 1gb).

7. Once you've entered a number, your hard drive will be repartitioned. After awhile it will reboot and re-initialize the stateful partition. This process takes 2-15 minutes and then the Chromebook reboots again and shows you the Welcome screen you got when you first turned on your Chromebook out of the cardboard box.

8. Go through the Chrome OS setup process again until you get to the Google login page. You'll need to have a WiFi or Ethernet connection again at this point. Now follow steps 2 through 4 again. This time the script will see that you've already made room for Ubuntu and start downloading ChrUbuntu.

    Pro Tip: Here's where you can install other versions of Ubuntu! Just specify the preferred Ubuntu flavor and version at the end of the   command:

        curl -L -O https://raw.githubusercontent.com/jalessio/chrubuntu-script/master/chrubuntu-install.sh; sudo bash chrubuntu-install.sh [flavor] [version] [target-disk]
    
    For example:

        curl -L -O https://raw.githubusercontent.com/jalessio/chrubuntu-script/master/chrubuntu-install.sh
        sudo bash chrubuntu-install.sh xubuntu-desktop lts

    this will install Xubuntu and the latest LTS release (14.04 as of writing).

9. During the installation (within the first 5-15 minutes). You'll see a few prompts to select your encoding, locale and language. For most people, the defaults should be fine, just press Enter but change them if you'd like.

10. After all of the Ubuntu files have been downloaded, installed and configured, the script will make a few more updates and then prompt you to reboot.

11. You'll see ChrUbuntu start up! The username is "user" and the password is "user".

12. Right now, you're in ChrUbuntu but if you reboot, you'll be back in Chrome OS. This is a safety feature, if ChrUbuntu won't boot, you want to be able to get back into Chrome OS to fix it. To make ChrUbuntu the default, run:

        sudo cgpt add -i 6 -P 5 -S 1 /dev/sda

    on the ARM Chromebook, replace /dev/sda with /dev/mmcblk0. The password is "user". It should be possible to run this from ChrUbuntu or Chrome OS.

    To make Chrome OS the default again, either turn off Developer Mode, or run:

        sudo cgpt add -i 6 -P 0 -S 1 /dev/sda
