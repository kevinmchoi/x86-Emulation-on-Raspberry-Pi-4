# x86-Emulation-on-Raspberry-Pi-4

Section 1.0 – Setup Bill of Materials
Section 1.1 – Hardware
1.1.1.	Raspberry Pi 4B
- 	https://www.raspberrypi.org/products/raspberry-pi-4-model-b/ 
1.1.5.	32GB microSD card (must be at least 32GB)
- 	https://www.oempcworld.com/OEMPCworld-com/500316.html 

Section 1.2 – Software
1.2.1.	Raspbian OS on 32GB microSD card
- 	Raspbian Buster OS 2021-01-11 at the time of writing this:
-	 https://drive.google.com/file/d/1nL8H-wu_H6jeNQ4ItSB0ZrSzS_bqyGoI/view?usp=drive_link

Section 2.0 – Setup x86 environment on ARM system
2.1.	Put Raspbian OS (item 1.2.1) on 32GB microSD card (item 1.1.5).
2.2.	Run this command on the Raspberry Pi: sudo nano /etc/apt/sources.list

      Make sure to comment out this line: 
      #deb http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi
      Please make sure to add these two lines:
      deb http://raspbian.raspberrypi.org/raspbian/ oldoldstable main contrib non-free rpi
      deb http://raspbian.raspberrypi.org/raspbian/ oldoldstable main
      
      Press Ctrl+S to save changes. Press Ctrl+X to exit.
2.3.  Run these commands on the Raspberry Pi:
      sudo apt-get update
      sudo apt-get install qemu-user-static binfmt-support debootstrap binutils gparted
      sudo debootstrap --foreign --arch i386 stretch ./chroot-stretch-i386 https://archive.debian.org/debian-archive/debian 
      sudo mount –t sysfs fys ./chroot-stretch-i386/sys/
      sudo mount –t proc proc ./chroot-stretch-i386/proc/
      sudo mount –bind /dev ./chroot-stretch-i386/dev/
      sudo mount –bind /dev/pts ./chroot-stretch-i386/dev/pts/
      sudo mount –bind /dev/shm ./chroot-stretch-i386/dev/shm/
      sudo cp /usr/bin/qemu-i386-static ./chroot-stretch-i386/usr/bin/
      sudo chroot ./chroot-stretch-i386/ /debootstrap/debootstrap --second-stage
2.4.  Reboot the Raspberry Pi to apply changes!
