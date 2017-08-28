## Status

I'm placing this project on hold for a few days whilst I decide what to do with it.

## Install / Update

###### Supported Linux Distributions

### Working
- ArchLinux
- Debian
- Gentoo
- Ubuntu

### Broken
- Fedora

###### Bootstrap ISO

1.  Setup a Linux environment (Virtualbox + Ubuntu LiveCD is a quick option.) An existing Linux install using any of the above listed distros will work also. Please **make sure** /var has at least 20GB available and /root has at least 10GB available.

2.  Download your ISO to this Linux machine – you can do this using: `wget http://url.here/file.iso`. Please be aware that the ansible script determines the distro by using the filename - this means that if you are using, for example, Ubuntu - your filename should contain this string.

3.  Run the following to build the ISO (replacing ISO_FILENAME with the actual name of the file.)

        git clone https://github.com/cawilliamson/ansible-gpdpocket.git
        cd ansible-gpdpocket
        sudo bash bootstrap-iso.sh ISO_FILENAME

4.  Write the file to USB by running the following (replacing USB_DEVICE with the actual device path for your USB drive):

        fdisk -l /dev/sd* # find the disk ID of your USB drive and use in command below.
        dd bs=1M if=~/bootstrap.iso of=USB_DEVICE

5.  Boot your GPD Pocket using the USB drive and you should have a completely working installer for your distribution of choice.

###### Bootstrap system

In order to install my Ansible playbooks on an existing install (e.g. one which you've set up with the `nomodeset fbcon=rotate:1` kernel parameters) please complete the following steps:

1.  Start by downloading the latest ZIP of my ansible playbooks from:  
    https://github.com/cawilliamson/ansible-gpdpocket/archive/master.zip

2.  Copy this file to a USB drive and insert that drive in to the GPD Pocket

3.  Mount the USB drive somewhere (`mount /dev/sda1 /mnt` for example)

4.  Using `cd` navigate to that new directory (for example: `cd /mnt`)

5.  Run the following command:

        sudo bash bootstrap-system.sh

###### Update system

1. Run `sudo gpd-update` – be aware that this process can take multiple hours if there is a kernel update available since it will be compiled on the GPD Pocket.

2. Reboot if any changes were made to ensure they get applied properly.

## Known Issues

###### All

- Distorted audio (kernel bug – https://bugzilla.kernel.org/show_bug.cgi?id=196351 )
- Suspend Issues (Enhancement: [#34](https://github.com/cawilliamson/ansible-gpdpocket/issues/34))
- USB-C Data Connectivity (hansdegoede is working on this currently)

###### Debian

- Neither netimage nor LiveDVD images can be used to run bootstrap-iso against due to differences in the on-disk file structure (and the fact that netimage installers have no files to patch!)
- When installing you will be informed modules cannot be loaded. If you select "Yes" to continue anyway this will allow you to continue. (Enhancement: [#22](https://github.com/cawilliamson/ansible-gpdpocket/issues/22))

###### Fedora

- Currently the Fedora installer is broken - please do not attempt to use this until I have removed this note. (Bug: [#66](https://github.com/cawilliamson/ansible-gpdpocket/issues/66))
- When installing Fedora you will need to select the option **without** the media checking functionality. Performing a media check will result in a checksum failure. (Enhancement: [#21](https://github.com/cawilliamson/ansible-gpdpocket/issues/21))

###### Solus

- i2c-tools is not presently on Solus, so the power task can't presently be run.

## Contributors

- efluffy at https://github.com/efluffy/gpdfand – great work on actually getting the fans in this thing to work.
- hansdegoede at http://hansdegoede.livejournal.com/17445.html – absolutely EVERYTHING related to the kernel was this guy.
- linuxiumcomau at http://linuxiumcomau.blogspot.com/ – inspired my work on bootstrapping install isos.
- stockmind at https://github.com/stockmind/gpd-pocket-ubuntu-respin – various code contributions and ideas.

## Donate

If this project helped you – feel free to buy me a beer (I could sure use a few!)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JGZUV7JA5A44E)
