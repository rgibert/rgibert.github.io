---
title: Wireless Android Debug Bridge (ADB)
tags:
    - adb
    - android
    - debugging
    - code
---

# Wireless Android Debug Bridge (ADB)

- Install [Android Platform Tools](https://developer.android.com/studio/releases/platform-tools).
- Enable Developer tools on the Android device.
- Enable "Wireless Debugging" on the Android device.
- Pair ADB
~~~ bash
adb pair host:port
~~~
- Connect ADB
~~~ bash
adb connect host:port
~~~
