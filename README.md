# teslausb upload directly to a OneDrive folder

## Intro

Using marcone/teslausb and barjohn/MarconeTeslausb I was able configure a Raspberry Pi Zero2 W so that your Tesla thinks it's a USB drive and will write dashcam footage to it. And sync to a Microsoft OneDrive folder using rclon:

- automatically copy the recordings to an archive server when you get home
- hold both dashcam recordings and music files
- automatically repair filesystem corruption produced by the Tesla's current failure to properly dismount the USB drives before cutting power to the USB ports
- serve up a web UI to view or download the recordings
- retain more than one hour of RecentClips (assuming large enough storage)


If you are interested in having more detailed information about how TeslaUsb works, have a look into the [wiki](https://github.com/marcone/teslausb/wiki).

## Prerequisites

### Assumptions

- You park in range of your wireless network.
- Your wireless network is configured with WPA2 PSK access.

### Hardware

Required:

- RasberryPi Zero 2 W
- A micro SD card, I used 256GB

Optional:

- a case for the pi

## Installing

[Set Up](doc/SetUp.md) 

## Contributing

You're welcome to contribute to this repo by submitting pull requests and creating issues.
For pull requests, please split complex changes into multiple pull requests when feasible, and follow the existing code style.

## Meta

This repo contains steps and scripts originally from [this thread on Reddit](https://www.reddit.com/r/teslamotors/comments/9m9gyk/build_a_smart_usb_drive_for_your_tesla_dash_cam/)

Many people in that thread suggested that the scripts be hosted on GitHub but the author didn't seem interested in making that happen, so GitHub user "cimryan" hosted the scripts on GitHub with the Reddit user's permission.
