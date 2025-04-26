# Gathering AMD-specific stuff

We'll be using OpenCore (obvi, like c'mon who rocks Clover in the BIG 2025) and, as the Dortania's guide doesn't have much details about the AMD specifics, mine will.

### Kexts

#### SMCAMDProcessor

Used for:

* CPU power management for AMD Zen (!) processors.
* Supports for reading of temperature, energy and frequency data on AMD Zen Processors.
* Manual switching of processor speed.
* PState editing.

(!) - No, do not try to run it on Athlons, plzzz.

Doesn't limit your macOS choice.

[GitHub](https://github.com/trulyspinach/SMCAMDProcessor)

#### USBToolBox

You will need to actually map your USB ports before booting into macOS recovery.  For this, you will need Windows 10/11 running on your machine.&#x20;

No, you can't use the same UTBMap.kext you've downloaded from someone else's EFI as your motherboards' USB layout is DIFFERENT.&#x20;

No, you can't just put in the USBInjectAll kext by ReHabMan and rock with it. Firstly, it'll most likely not work on AMD. Secondly, it didn't recieve any updates since 2018, and is:

1. A possible security threat
2. Unstable and might cause issues

The USBToolBox usage is simple. Download the latest kernel extension from [here](https://github.com/USBToolBox/kext/releases/), download the [tool](https://github.com/USBToolBox/tool/releases/) while you're in it, throw the kext into your `EFI\OC\Kexts` directory, then open the tool, grab a USB flash stick or whatever easily-removable device you've got and stick it inside all of your USB ports port by port, changing the port once the text in your console window refreshes.&#x20;

[GitHub](https://github.com/USBToolBox)

#### RestrictEvents

For most users, this kext will make your "About this Mac" look normally, f.e like this, and not like a total mess.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-26 at 07.13.54.png" alt=""><figcaption></figcaption></figure>

[GitHub](https://github.com/acidanthera/RestrictEvents)

#### AppleMCEReporterDisabler

Is required to normally boot into macOS since 12.3 all the way up to the present.&#x20;

Download[^1]

#### XLNCUSBFix

Required for proper USB functioning on AMD FX systems.

[Download](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/XLNCUSBFix.kext.zip)

#### VoodooHDA

Fixing audio on AMD FX systems. Needs SIP to be off since macOS Big Sur.

[SourceForge](https://sourceforge.net/p/voodoohda/code/HEAD/tree/)



### SSDTs

I recommend creating your SSDT's yourself using [SSDTTime](https://github.com/corpnewt/SSDTTime) by corpnewt. Considering we're rocking AMD, we only need 3

| SSDT                                                                                                              | Who needs this                                                                                     | Why                                                                |
| ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| [SSDT-CPUR](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) | <p>Required for B550, A520 and newer for Zen CPUs</p><p>Threadripper-based PC's dont need it. </p> | Fixes CPU definitions in ACPI                                      |
| SSDT-EC                                                                                                           | Everyone, however laptop and desktop versions are different.                                       | To create a fake Embedded Controller that macOS can interact with. |
| SSDT-USBX                                                                                                         | Everyone                                                                                           | Provides generic USB power properties                              |

Dortania also has a pre-compiled [SSDT-EC-USBX-DESKTOP.aml ](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)if you're too lazy to build the upper two using SSDTTime&#x20;

### Vanilla patches

These are REQUIRED. Without these, your setup will NOT run. You will need to patch the bootloader according to how many cores you have. Use the README.md for reference and for instructions on how to do this.

{% hint style="info" %}
Note: we are talking about CORES, not threads. So if you're on Ryzen 5, for instance, you have 6 cores and 12 threads, and you'll use the number 6 in patching. Got it? Thank you!
{% endhint %}

[GitHub](https://github.com/AMD-OSX/AMD_Vanilla)

### Apps

1. [AMD Power Gadget](https://github.com/trulyspinach/SMCAMDProcessor) to control fan speeds, measure loads, etc.
2. Maybe some others?



Once all of that is downloaded, head back to Dortania's [Gathering Files](https://dortania.github.io/OpenCore-Install-Guide/ktext.html) and collect the shit you need for your hardware.



[^1]: 
