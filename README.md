iDroid Project openiBoot
---------------------------------------------------
	Copyright (C) 2008 David Wang (planetbeing).

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

NOTE: Version 0.3 and above will not boot iDroid 2.6.32 series kernels without additional parameters being passed to the kernel.

Warnung
---------------------------------------------------
IT IS STRONGLY ADVISED THAT YOU DO NOT ATTEMPT TO RUN NAND WRITE FUNCTIONS IN THE A4 VERSION AT THIS POINT IN TIME.

DOING SO WILL INEVITABLY CAUSE YOU TO NEED TO RESTORE YOUR DEVICE, MAY LEAVE PERMANENT NAND BLOCK DAMAGE AND MAY ALSO CAUSE GREMLINS TO CRAWL OUT OF YOUR ARSE.

(If you read this warning properly, really unless you know wtf you are looking at - leave it alone until we stablise it)

Compiling on Arch (with AUR)
---------------------------------------------------
To run openiboot from recovery mode (a.k.a iboot), you’ll need to create an img3 image.
To run openiboot from DFU mode, you'll need to create a bin.

Build requires make, scons, libssl, libpng, libcurl, libusb, libreadline and pthread.
In addition, you will need xpwn-nyuszika7h-git and arm-linux-gnueabihf-gcc from AUR.

Example:
```
CROSS=arm-linux-gnueabihf- PLATFORM=IPHONE4 make -j24
```

Menu Configuration
---------------------------------------------------
As of version 0.3 OpeniBoot now has a grub-style configurable menu system, OpeniBoot looks for /boot/menu.lst at boot.
Below is an example menu.lst - put it in /boot (This section will be expanded upon at a later date, when newer device ports are further ahead)

	title iOS
	auto

	title Android
	kernel "(hd0,1)/idroid/zImage" "console=tty root=/dev/ram0 init=/init rw"
	initrd "(hd0,1)/idroid/android.img.gz"

	title iX
	kernel "(hd0,1)/iX/zImage" "console=tty root=/dev/ram0 init=/init rw"
	initrd "(hd0,1)/iX/initrd.img.gz"


Reporting issues/requesting features
--------------------------------------------------
Please leave bug reports/pull requests in the Github tracker.

For anything else, we can be found lurking in #idroid-dev on irc.freenode.net
