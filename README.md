<h1>macOS Big Sur on Dell Latitude 5300 with OpenCore</h1>

![1](https://user-images.githubusercontent.com/37314164/136286445-4b590715-c9be-4e03-99d1-08d51f56a410.png)
![2](https://user-images.githubusercontent.com/37314164/136286453-e775a087-9bc7-4e76-a67a-93d18594637b.png)

## Important

This repo has things specific to my laptop. It should work in a identical computer, but maybe it won't.

## Instructions

You **must** add your own serialnumber. I recommend [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Remember to use `MacBookPro15,2`. 

Use this a a starting point, this is no replacement of your own research, trial and error.

Remove kexts asociated with BCM94352Z(DW1560) if you do not have installed one, and do a Snapshot in ProperTree to remove them from config.plist.

## What is working

### Completely supported

#### Audio

Audio on speakers and headphones works as intended.

#### CPU

XCPM power management is native supported. HWP is fully enabled as well. Added cpufriend for more energy savings.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo so I replaced mine with BCM94352Z (DM1560). 
Airport, Handoff are working correctly.

###### Important: If you have an Intel card, remove BCM-related kexts, rescan with ProperTree and start from there.

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

Fan Speed, CPU temp and voltage.

### Partially working

#### Touchpad

Functioning with multigestures. But buttons only work if your finger is pressing the touchpad.

### Not working

Not tested enough to find problems...yet

### Not tested

#### Sleep and Wake

Sometimes weird behavior happens. Example, if a key if pressed when the laptop is waking up from sleep, the keyboard will stop responding, and the key pressed will repeat indefinitely in the password field, the touchpad also dies.

A workaround i've found is when the laptop wakes from sleep, do not press any key inmediately. Wait 5-10 seconds then start typing, that works for me, but sometimes the touchpad just quits anyway.

#### Others

Internal SD card Reader

#### Keyboard

Brightness keys not working. Also strange behavior sometimes after waking up, see Sleep.


## Additional info, quirks, findings, etc 

You can adapt this repo to Catalina, you should change Min/MaxVersion to -1, and change your SecureBootModel. I am targeting Big Sur and newer only though.

### TODO:

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
      <td>TBD</td>
    </tr>
    <tr>
    </tr>
  </tbody>
</table>

## Changelog

##### 06/oct/2021:

Updated to OpenCore 0.7.4

Added README

Removed unnecesary clutter, checked config.plist against Sample.plist and ocvalidate.

##### 04/oct/2021:

First release, minimal not tested.

