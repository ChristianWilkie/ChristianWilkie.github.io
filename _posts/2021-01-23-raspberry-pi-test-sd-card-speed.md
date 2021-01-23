---
layout: post
title: Raspberry Pi - Test SD Card Speed
date: 2021-01-23 13:59 -0500
---

Recently I was messing around with my Raspberry Pi 4 again, and I was looking to test the read/write speed of the USB stick I have it booting off of now. It's a generic, unbranded 16gb USB stick that I have plugged into one of the USB 3.0 ports, running Raspbian.

Here's an easy way to do it if you're in a similar position (works for SD card, SSD, etc too):

First we test the write speed by writing 500MiB:

`dd if=/dev/zero of=~/test.tmp bs=500K count=1024 oflag=dsync`

You should see something like:

```
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 121.854 s, 4.3 MB/s
```

To test the read speed, we're going to read the file that we just wrote - but first we need to discard the disk caches (requires sudo):

```
sync; echo 3 | sudo tee /proc/sys/vm/drop_caches
```

Don't skip this! Otherwise you might get inaccurate results like 500mb/s

Next test the read speed:

`dd if=~/test.tmp of=/dev/null bs=500K count=1024`

You should see something like this:

```
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 19.2854 s, 27.2 MB/s
```

If you want a simple script to run, here's a version of the above that can be ran to sudo, writes out the file to /tmp, and cleans up after itself: <https://gist.github.com/ChristianWilkie/b450783afea4e666fb2e1c16e34e7e1d>

```
chmod +x ./speed.sh
sudo ./speed.sh
```

speed.sh:
```
#!/bin/bash
# Tests Raspberry Pi disk read/write speed

if [ "$EUID" -ne 0 ]
  then echo "Please run as root"
  exit
fi
echo "=== Performing Write Speed Test ==="
dd if=/dev/zero of=/tmp/test.tmp bs=500K count=1024 oflag=dsync
sync; echo 3 | tee /proc/sys/vm/drop_caches
echo "=== Performing Read Speed Test ==="
dd if=/tmp/test.tmp of=/dev/null bs=500K count=1024
rm -rf /tmp/test.tmp
echo "=== Speed Test Complete ==="
```

Output for my USB drive:
```
chris@raspberrypi:~$ sudo ./speed.sh 
=== Performing Write Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 107.547 s, 4.9 MB/s
3
=== Performing Read Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 23.0081 s, 22.8 MB/s
=== Speed Test Complete ===
```

Comparing it with the output for my SD Card (SanDisk 128GB Ultra C10 A1):
```
chris@raspberrypi:~$ sudo ./speed.sh 
=== Performing Write Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 32.9342 s, 15.9 MB/s
3
=== Performing Read Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 11.9345 s, 43.9 MB/s
=== Speed Test Complete ===
```

Turns out that USB drive probably isn't too great for running the OS compared to the SD card.

I also had a very old SSD lying around so I thought I'd test that out. It's using a generic USB->SATA cable, it shows up in lsusb as:
`Bus 003 Device 038: ID 174c:55aa ASMedia Technology Inc. ASM1051E SATA 6Gb/s bridge, ASM1053E SATA 6Gb/s bridge, ASM1153 SATA 3Gb/s bridge, ASM1153E SATA 6Gb/s bridge`
and using `sudo smartctl -a /dev/sde` some of the disk information shows up as:

```
Model Family:     Crucial/Micron RealSSD m4/C400
Device Model:     M4-CT128M4SSD2
Firmware Version: 000F
User Capacity:    128,035,676,160 bytes [128 GB]
```

I tried using the gnome-disk-utility built in to my desktop's Ubuntu to check the drive before trying it in my Raspberry Pi:

![gnome-disk-utility results for Crucial M4 128GB drive](/assets/posts/2021/01/23/m4-ssd-disk-util-benchmark.png)

Crucial M4 128GB speed test results:
```
=== Performing Write Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 14.6738 s, 35.7 MB/s
3
=== Performing Read Speed Test ===
1024+0 records in
1024+0 records out
524288000 bytes (524 MB, 500 MiB) copied, 1.61269 s, 325 MB/s
=== Speed Test Complete ===
```

So, actually the SSD performs really, really well! Kinda cool I was able to get some new use out of this otherwise unused SSD :)

References:
1. <https://www.thomas-krenn.com/en/wiki/Linux_I/O_Performance_Tests_using_dd>
2. <https://elinux.org/RPi_SD_cards#SD_card_performance>
3. <https://www.raspberrypi.org/forums/viewtopic.php?t=31925>