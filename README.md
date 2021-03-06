# Installing Lubuntu on the Asus UX305LA
My UX305LA model has a Broadwell i5-5200U processor, 256GB SSD, 8GB RAM, and 1920x1080 display.

I wanted to install Lubuntu alongside Windows 10. Since all Windows 10 hardware has UEFI and Secure Boot, it can complicate things for those who want to dual boot Windows and Linux. Luckily the major distributions (including Ubuntu) have adapted their installations to accomodate such hardware. However, for Lubuntu (and presumably Ubuntu), only the 64-bit version works with UEFI and Secure Boot. I tried the 32-bit version, and it would only install if I first enabled CSM (Compatibility Support Module) in the BIOS. However, I have read that installing a Linux distribution alongside Windows 10 in this way (i.e. not in UEFI mode) can cause issues for those who do not have a solid understanding of BIOS and UEFI.

~~All that said, I settled on Lubuntu 15.04, 64-bit (I tried 15.10 but had issues with suspending the laptop - the laptop would suspend, but then become unresponsive upon waking).~~ I am using Lubuntu 16.04, 64-bit. For installation, I chose the "install alongside Windows" option, and shrunk the Windows partition. After installation, here are things that work immediately:

- Wi-Fi
- Touchpad (though required further tweaking according to personal preferences)
- Power button
- Suspend
- Monitor off key (fn-F7)
- Print screen (saves to ~/ directory)
- Webcam

Things that require additional configuration or workarounds:

- Suspend shortcut (fn-F1)
- Suspend after idle period (will unsuccessfully try to hibernate instead; prompt asking for password before hibernation shows)
- Airplane mode (fn-F2)
- Brightness adjustment (fn-F5, fn-F6). Though ctrl-F10 and ctrl-F11 will dim and brighten.
- Trackpad toggle (fn-F8)
- Sound
- Sound adjustment and mute (fn-F10, fn-F11, fn-F12)
- Getting the sound to work
- Getting the microphone to work

## Trackpad tweaks
Add the following lines to `~/.config/lxsession/Lubuntu/autostart` (it was an empty file before editing)
```
synclient TapButton3=2
synclient ClickFinger3=2
synclient FingerHigh=17
synclient FingerLow=10
synclient MaxTapMove=20
synclient HorizHysteresis=10
synclient VertHysteresis=5
synclient VertEdgeScroll=0
synclient AreaLeftEdge=200
synclient AreaRightEdge=2800
synclient AreaTopEdge=250
synclient VertScrollDelta=30
synclient CoastingSpeed=0
synclient PalmDetect=1
synclient PalmMinWidth=3
synclient PalmMinZ=100
synclient MaxTapTime=200
synclient MaxSpeed=2
synclient AccelFactor=0.1
```
Adjusts speed/sensitivity, adds three finger tap/click, removes edge scrolling, disables coasting (continued two-finger scrolling even after lifting fingers), makes touchpad less sensitive to unwanted clicks/movement while typing. Since the options are in the `autostart` file, they will automatically be applied at startup.

Also add the following line to disable tapping and scrolling (mouse movement and clicks still register) for 0.5 seconds after any keyboard press. Modifier keys such as alt, shift, and ctrl will not count as keyboard presses.

```
syndaemon -i 0.5 -d -t -K
```

## Sound tweaks
To get sound and microphone working, install pulseaudio (`sudo apt-get install pulseaudio`), pavucontrol, and pavumeter (`sudo apt-get install pavucontrol pavumeter`) and play with the settings until sound works. Installing pulseaudio should also allow one to add the sound indicator to the taskbar.

To get the shortcuts working, open up `~/.config/openbox/lubuntu-rc.xml` and search for the following:

- `XF86AudioRaseVolume`
- `XF86AudioLowerVolume`
- `XF86AudioMute`

Then edit the text between `<command>` and `</command>` for each of the three respective sections to

- `amixer -D pulse -q sset Master 3%+ unmute`
- `amixer -D pulse -q sset Master 3%- unmute`
- `amixer -D pulse -q sset Master toggle`

## Changes to openbox settings
#### Shortcuts for resizing windows
For aerosnap-like functionality, open up `~/.config/openbox/lubuntu-rc.xml` and search for the following:

- `"W-Left"`
- `"W-Right"`
- `"W-Up"`

Then make the following changes for each of the three searches:

- Make sure "height" is set to `100%` and "width" is set to `50%`
- Make sure "height" is set to `100%` and "width" is set to `50%`
- Change `action name` to `"Maximize"` (include the quotes)

For some reason the "snap left" and "snap right" functionality doesn't work perfectly for the terminal programs I've tried so far (XTerm and LXTerminal). The windows snap correctly, and take up 50% of the horizontal space; however, they don't extend all the way down and leave a small gap from the bottom.

#### Disable some desktop switching shortcuts
There are a few desktop switching keyboard shortcuts that I don't use, and which clash with shortcuts I use in other programs

Comment out shortcuts for `C-A-Up`, `C-A-Down`, `S-A-Up`, and `S-A-Down`

## Miscellaneous
After installing `texlive`, a package called `prerex` becomes the default program for opening `.tex` files. Doing so will force a system logout though. Appears to be an issue with the `prerex` package itself. For workaround just reset default for `.tex` files to something else.

## Software to install
Partial list

- R
- RStudio
- Chrome
- Dropbox
- texlive-full
- pandoc
