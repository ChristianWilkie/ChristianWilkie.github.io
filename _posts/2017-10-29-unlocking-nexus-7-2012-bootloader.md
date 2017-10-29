---
layout: post
title:  Unlocking Nexus 7 2012 Bootloader
date:   2017-10-29 03:38:35
---

1. Install the latest android sdk from <https://developer.android.com/studio/index.html#downloads>
2. Install the google usb driver from <https://developer.android.com/studio/run/win-usb.html>
3. On your Nexus 7: enable developer settings by going to "Settings", "About phone", scrolling down to the "Build number" and tapping it 7 times. Next go to "Settings", "Developer Options", "USB debugging" and enable it.
4. Connect your Nexus 7 to your PC and click "Ok" on the "Allow USB debugging?" prompt that pops up on your Nexus 7. 
5. Open a command prompt in the platform-tools directory of your android sdk. Type `adb devices` and you should see your Nexus 7 listed. 
6. Enter `adb reboot bootloader` to boot into the bootloader. 
7. Type `fastboot oem unlock` and press enter. 
8. A menu will popup on the Nexus 7 - select "yes" with the volume up/down and power buttons. On the bottom of the screen you should see lock state: unlocked!