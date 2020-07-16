---
title: USB Boot Disk
description: Burn an iso to a usb boot disk
published: true
date: 2020-07-04T06:28:01.890Z
tags: 
editor: undefined
---

# Creating a USB boot disk

Using the command line, an iso image can be burnt to a usb drive using the following:
- Firstly, check where the device is mounted using lsblk:
```
lsblk
```
The drive will be located at **/dev/sdb** or similar. To copy the iso to the drive, use the following:
```
sudo umount </dev/sdb>
sudo dd if=</path/to/ubuntu.iso> of=</dev/sdb> bs=1M
```
> Make sure **/deb/sdb** is the correct path to the usb device.
{.is-warning}
