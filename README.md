<h1>macOS Catalina / Big Sur on Dell Latitude 5300</h1>

<img width="1440" alt="Captura de Pantalla 2021-12-29 a la(s) 02 47 41 copia" src="https://user-images.githubusercontent.com/37314164/147631372-951b1c13-fa46-4731-9e41-aa1249ab5095.png">

<img width="698" alt="Captura de Pantalla 2021-12-29 a la(s) 02 45 57" src="https://user-images.githubusercontent.com/37314164/147631363-6cad6b8c-641b-4898-8de2-277bceee37d2.png">

This repo has things specific to my laptop. It should work in a identical computer, but maybe it won't.

## Instructions

You **must** add your own serialnumber. I recommend [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Remember to use `MacBookPro15,2`. 

Use this a a starting point, this is no replacement of your own research, trial and error.

Remove kexts asociated with BCM94352Z(DW1560) if you do not have installed one, and do a Snapshot in ProperTree to remove them from config.plist.

### Fixing audio

1. Download ALC295PlugFix.zip from releases.
2. Uncompress into a directory in your home folder ( ~/ALC295PlugFix/)
3. Copy ALCPlugFix-Swift to /usr/local/bin/
4. Copy com.black-dragon74.ALCPlugFix.plist into /Library/LaunchAgents
5. Open a terminal and cd into the uncompressed folder
6. Execute install.sh (./install.sh)
7. When prompted, drag ALC295.plist file to terminal, press enter
8. Open your config.efi and add 'alc-verbs=1' to bootargs
9. Reboot and test

This should solve the headphones problem (it worked for me in Catalina).

## What is working

### Completely supported

#### CPU

XCPM power management is native supported. HWP is fully enabled as well. Added cpufriend for more energy savings.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo so I replaced mine with BCM94352Z (DM1560). 
Airport, Handoff are working correctly.

Important: If you have an Intel card, remove BCM-related kexts, rescan with ProperTree and start from there.

#### Camera

Camera is functioning normally.

#### USB

USB ports are working as expected.

Use USBInject-All.kext then with Hackintool disable all unused ports and generate a USBPorts.kext

#### Ethernet

Functioning normally.

#### Display and External Monitors

Working fine with hardware acceleration. External monitors work fine over USB-C docking stations.

#### Battery

Detected and correct values.

#### Sensors

Fan speed, CPU temp and voltage.

### Partially working

#### Touchpad

Functioning with multigestures. But buttons only work if your finger is pressing the touchpad.

#### Audio

Audio on speakers works as intended. But using headphones requires an ugly workaround.

### Not working

Not tested enough to find problems...yet

### Not tested

#### Sleep and Wake

Sometimes the laptop crashes when sleeping, not common but it happens.

#### Internal SD card Reader.

There are kexts included but i dont have card to test, so those are disabled.

#### Keyboard

Brightness keys not working, BrightnessKeys kext included but doesn't work and produces lag or weird behavior. Disabled


## Additional info, quirks, findings, acknowledgements, etc 

Secure Boot is Disabled, but you should enable with an ECID value for full security.

This thing has me pulling my hair in rage and frustration. Sometimes kernel_task decides to use 60-70% of the CPU with no reason. I don't know how to debug, and no cause has been found. For now I have only the most essential kexts loaded and the problem has almost dissapeared, but happens. I've tried from Catalina to Monterey, and it appears. If you have this problem and found a solution please open a pull request or issue.

If you have the 1080p panel, use [one-key-hidpi](https://github.com/xzhih/one-key-hidpi). The application gives you two options, normal and EDID. Use EDID, otherwise you wont have backlight.

### Quirks about audio:

If the device is added via `DeviceProperties -> Add` the laptop produces an awful noise in the headphones until the daemon is launched. The workaround is making audio work using `alcid=28`

Also this command fixes the audio.

`./alc-verb 0x19 0x707 0x24 & ./alc-verb 0x1a 0x707 0x20`

The downside is it has to be issued every time a headphone is connected.

### Acknowledgements

[Mrgeque@tonymacx86](https://www.tonymacx86.com/threads/guide-dell-inspiron-15-7573-catalina-10-15-7-oc-0-6-0-i7-8550u-4k-uhd-620-best-100-simple-setup.305350/page-11): For his PlugFix which worked wonders.

[SamWRLD_@reddit:](https://www.reddit.com/r/hackintosh/comments/q7yv6n/latitude_5300_screen_with_no_brightness_until/hikkt37/) For sending me a EFI folder which i used to compare and fix some of my bugs.

OpenCore, Clover developers, Acidanthera: Thanks for making hackintoshes tick.

//RANT: This laptop is just too hot to be comfortable to work with, just buy a M1 Air.

## TODO:

A lot of things, mostly testing, but I consider this repo to be just fine for daily use.

<h2>Laptop Specs</h2>
<table>
  <thead>
    <tr>
      <td style="text-align: center">Feature</td>
      <td style="text-align: center">Specification</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Model</td>
      <td>Dell Latitude 5300</td>
    </tr>
    <tr>
      <td>CPU</td>
      <td>Intel Core i7-8665U</td>
    </tr>
     <tr>
      <td>GPU</td>
      <td>Intel UHD Graphics 620</td>
    </tr>
    <tr>
      <td>Audio</td>
      <td>Realtek ALC295, layout-id 28</td>
    </tr>
    <tr>
    </tr>
  </tbody>
</table>

## Changelog

29/dic/2021:

Audio headphone fixes.

Updated OpenCore -> 0.7.6, and kexts to their latest versions.

Updated README.

##### 06/oct/2021:

Updated to OpenCore 0.7.4

Added README

Removed unnecesary clutter, checked config.plist against Sample.plist and ocvalidate.

##### 04/oct/2021:

First release, minimal not tested.

