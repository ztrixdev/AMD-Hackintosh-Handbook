# Choosing your hardware and OS

### The iGPU problem

You can never go wrong with a Vega... Untill the Vega is an iGPU and not a dGPU.  In your build, you either turn off your iGPU entirely in the boot-args, meaning that you will be stuck with your dGPU only, which is fine in most cases, or you use your Vega iGPU with the [NootedRed kext](https://chefkissinc.github.io/applehax/nootedred/), and remove WhateverGreen which will make you unable of using your dGPU.

{% hint style="info" %}
Note: You'll most likely fail with trying to make your old-ass Athlon G iGPU work. Just go Ryzen or get a dGPU.
{% endhint %}

### Choosing your macOS version

| AMD CPU family                   | The lowest you can go    | The highest you can go |
| -------------------------------- | ------------------------ | ---------------------- |
| FX, Athlon, Opteron              | macOS 10.13 High Sierra  | macOS 12 Monterey      |
| Ryzen, Threadripper              | macOS 10.13 High Sierra  | macOS 15 Sequoia       |
| If you plan on rocking your iGPU | macOS 10.15 Catalina     | macOS 14 Sonoma        |
