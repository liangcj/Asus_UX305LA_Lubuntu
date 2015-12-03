# Installing Lubuntu on the Asus UX305LA
My UX305LA model has a Broadwell i5-5200U processor, 256GB SSD, 8GB RAM, and 1920x1080 display.

I wanted to install Lubuntu alongside Windows 10. Since Windows 10 hardware all has UEFI and Secure Boot, it can complicate things for those who want to dual boot Windows and Linux. Luckily the major distributions (including Ubuntu) have adapted their installations to accomodate such hardware. However, for Lubuntu (and presumably Ubuntu), only the 64-bit version works with UEFI and Secure Boot. I tried the 32-bit version, and it would only install if I first enabled CSM (Compatibility Support Module) in the BIOS. However, I have read that installing a Linux distribution alongside Windows 10 in this way (i.e. not in UEFI mode) can cause issues for those who do not have a solid understanding of BIOS and UEFI.

All that said, I settled on Lubuntu 15.04, 64-bit (I tried 15.10 but had issues with suspending the laptop - the laptop would suspend, but then become unresponsive upon waking). For installation, I chose the "install alongside Windows" option, and shrunk the Windows partition. After installation, here are things that work immediately:

- Wi-Fi
- Touchpad (though required further tweaking according to personal preferences)
- Power button
- Suspend
- Monitor off key (fn-F7)
- Print screen (saves to ~/ directory)

Things that require additional configuration or workarounds:

- Suspend shortcut (fn-F1)
- Airplane mode (fn-F2)
- Brightness adjustment (fn-F5, fn-F6). Though ctrl-F10 and ctrl-F11 will dim and brighten.
- Trackpad toggle (fn-F8)
- Sound adjustment and mute (fn-F10, fn-F11, fn-F12)
- Getting the sound to work
