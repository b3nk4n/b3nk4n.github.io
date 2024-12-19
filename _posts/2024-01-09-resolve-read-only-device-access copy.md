---
title: Resolve Read-only Device Access
author: b3nk4n
categories: [Tools]
tags: [mac, linux, trick]
pin: false
---

On your MacBook (or Linux based device), external devices such as hard drives or SD cards might be mounted by default as read-only.
This could be due to different reasons, such as enforced by a device policy:

![You can only read](/assets/img/posts/2024/sd-read-only.png)
_Permission: You can only read_

However, if you need write access to that device to back up your data or similar, there is a simple workaround to resolve that.
By manually mounting the disk manually with both **read & write** access.

#### 1. Find the respective device

Any of the following CLI tools might help you to find the **device** or **mount point** of the device you are looking for:

```console
df -h
diskutil list
```

#### 2. Unmount the device

Assuming the device is called `/dev/disk7s1` with mount point `/Volumes/sdc` and uses FAT32 (like my SD card),
then use either of the following command to unmount it first:

```console
sudo umount /Volumes/sdc
diskutil unmount /dev/disk7s1
```

#### 3. Manually mount the device with read & write access

Finally, mount it once again, but with custom permissions:

```console
sudo mkdir /Volumes/sdc
sudo mount -o rw -t msdos /dev/disk7s1 /Volumes/sdc
```
Please note that `-o rw` is the option to enable both read and write access, and `-t msdos` defines the filesystem type to be FAT32.

![You have custom access](/assets/img/posts/2024/sd-custom-access.png)
_Permission: You have custom access_

Checking the device permissions once again reveals that the mention of _"You can only read"_ is gone. Great!
