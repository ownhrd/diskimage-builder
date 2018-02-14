Scripts based on Image building tools for OpenStack
===================================================

``diskimage-builder`` is a flexible suite of components for building a
wide-range of disk images, filesystem images and ramdisk images for
use with OpenStack.

Install
=======

`apt install python-pip python-setuptools debootstrap python-glanceclient python-novaclient qemu-utils kpartx git && pip install diskimage-builder`

Run build image
===============
* Add private key to /root/.ssh

* Create OpenStack Volume ~50GB and attach on building VM

  * `mkfs.ext4 /dev/sdX && mount /dev/sdX /mnt && cd /mnt`

  * `git clone https://github.com/ownhrd/diskimage-builder.git && cd diskimage-builder`

  * `sudo ./build-name-distrib`

Cron task example
=================
`SHELL=/bin/bash`

`PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`

`m h dom mon dow user	command`

`0 3 	* * * 	root	bash /mnt/diskimage-builder/auto-delete-old-image &> /var/log/auto-delete-old-image`

`30 0 	* * *	root	bash /mnt/diskimage-builder/build-centos6 &> /var/log/build-centos6`

`0 1 	* * *	root	bash /mnt/diskimage-builder/build-centos7 &> /var/log/build-centos7`

`30 1 	* * * 	root	bash /mnt/diskimage-builder/build-debian &> /var/log/build-debian`

`0 2 	* * *	root	bash /mnt/diskimage-builder/build-fedora24 &> /var/log/build-fedora24`

`30 2 	* * *	root	bash /mnt/diskimage-builder/build-ubuntu &> /var/log/build-ubuntu`
