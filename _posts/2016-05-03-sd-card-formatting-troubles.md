---
layout: post
title:  SD Card Formatting Troubles
date:   2016-05-03 22:53:24
---
Recently I was playing with my Raspberry Pi that was collecting dust in my closet and encountered a problem when trying to format the SD card. I downloaded the official SD formatter tool from https://www.sdcard.org/downloads/formatter_4/eula_windows/ but kept getting this error when trying to format my SD card: "The Memory Card is write-protected. Please release the write protect switch.". I tried toggling the write protect switch, ejecting the drive, etc but none of that seemed to help. After some searching I came across some instructions on using diskpart in Windows that finally fixed the issue. Here's what I did:

- Open run and type diskpart
- type LIST DISK
- identify the drive number of your SD card (for instance, if you have a 16GB card look for the disk that is ~14GB)
- type SELECT DISK X (where X is the disk number from the previous step)
- type ATTRIBUTES DISK CLEAR READONLY
- now type exit and then eject your sd card and re-insert it into your PC

![Diskpart utility window](/assets/posts/2016/05/03/diskpart.png "Diskpart utility window")

After doing the above with diskpart I was finally able to format my SD card! Hope this is helpful to someone else with the same problem :)