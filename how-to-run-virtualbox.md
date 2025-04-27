# How to run VirtualBox

### The problem

Not only does the AppleHV emulator not work on AMD CPU's because of Intel-specific instructions, moreover, the situation is worse than you might think.

Parallels 14+, VMware Fusion 11+ and VirtualBox 7+ are cooked. They (for some reason) rely on AppleHV and can't be run.&#x20;

However, with some tricks we can make VirtualBox 6.1 run on newer macOS versions (13+). The problem with it is that it needs to install a kernel extension that macOS will never allow on Ventura+. However, using AMFIpass.kext we can disable this limitation

{% hint style="info" %}
Note: this guide invovles disabling SIP (System Integrity Protection). This imposes security threats, but, if you don't work with software that requires SIP being enabled OR if you are not an idiot, you should be perfectly fine. Proceed with caution.
{% endhint %}

### Installing VirtualBox 6.1&#x20;

In this example, I'll be using my own machine that is working on macOS 14 Sonoma.

The first step is, of course, mounting our EFI partition. You can do this via [MountEFI](https://github.com/corpnewt/MountEFI) by corpnewt or inside the OpenCore configurator app, if you have it.&#x20;

After you mounted your EFI, throw the freshly-downloaded [AMFIPass.kext](https://github.com/bluppus20/AMFIPass/) into your `EFI\OC\Kexts` . It should look like this:

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.14.28.png" alt=""><figcaption><p><a href="https://github.com/ztrixdev/B550M-R5600x-RX580-OpenCore">My EFI folder</a>, if you're interested</p></figcaption></figure>

Then, using [ProperTree](https://github.com/corpnewt/ProperTree), perform an OC snapshot. If you can't, manually add the kext following this structure:

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.28.00.png" alt=""><figcaption><p>It can obvi be NOT Number 11 in your EFI, just make it the last .kext and that's it, omg.</p></figcaption></figure>

After you did it, reboot into recovery. We need to go into Utilities -> Terminal, then typing in this easy command: `# csrutil disable` . It should output `System Integrity Protection is off. Restart the machine for the changes to take effect.` Now you can hit your reset button and boot back into macOS.

Then, you go to the [VirtualBox website](https://www.virtualbox.org/) and follow these steps:

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.30.05.png" alt=""><figcaption><p>Scroll down</p></figcaption></figure>

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.30.16.png" alt=""><figcaption><p>Click on VirtualBox older builds</p></figcaption></figure>

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.30.25.png" alt=""><figcaption><p>Downlaod the 6.1.50 version for INTEL macOS (!)</p></figcaption></figure>

After you've finished downloading, simply install VirtualBox normally, allow the extensions to install:

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 03.31.30.png" alt=""><figcaption><p>Click Allow and enter your password</p></figcaption></figure>

Congrats! Now reboot your machine and you're ready to rock!

### Ideal VM build

The more resources you give the VM, the worse the performance will get. So stick to these limits:

* 4 GB RAM
* 4 CPU cores
* 1 GB VRAM

And it still doesn't unleash the full PoTeNtIaL, so, if you REALLY need productive VMs, stick to Linux.

And I use Arch in a VM, btw) XD

<figure><img src=".gitbook/assets/Screenshot 2025-04-27 at 06.00.14.png" alt=""><figcaption></figcaption></figure>
