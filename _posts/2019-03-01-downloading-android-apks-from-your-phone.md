---
layout: post
title: Downloading Android APKs from your phone
date: 2019-03-01 23:52 -0500
---

Some key commands:
```
adb shell pm list packages
adb shell pm path <package from above>
adb pull <path from above> <local path to download to>
```

Here's an example applied to Neko Atsume, the premier internet cat game:

```console
C:\Users\chris>adb shell pm list packages | grep neko
package:jp.co.hit_point.nekoatsume

C:\Users\chris>adb shell pm path jp.co.hit_point.nekoatsume
package:/data/app/jp.co.hit_point.nekoatsume-n4XAV9PPJIzObbfURWHm2A==/base.apk

C:\Users\chris>adb pull /data/app/jp.co.hit_point.nekoatsume-n4XAV9PPJIzObbfURWHm2A==/base.apk nekoatsume.apk
/data/app/jp.co.hit_point.nekoatsume-n4XAV9PPJIzObbfURWHm2...e.apk: 1 file pulled. 14.1 MB/s (19756023 bytes in 1.341s)
```

Happy Hacking 😺