---
title: FFMPEG - Speed up audio of a file
tags:
    - audiobooks
    - audio
    - multimedia
---

# FFMPEG - Speed up audio of a file

NOTE: ACCELERATION can be a value from "0.5" (1/2 speed) to "2.0" (double speed)

~~~ bash
ffmpeg -i INPUT_FILE -filter:a "atempo=ACCELERATION" -vn OUTPUT_FILE
~~~
