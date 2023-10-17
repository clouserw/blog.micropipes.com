---
layout: post
title: Setting up a Yaesu FTDX-3000 with FT8 on OS X
tags:
- radio
- walkthrough
---

There are plenty of walkthroughs online about setting up FT8 on the DX-3000 with Windows but I didn't find any for OS X.  So, here we are.  I'm using the USB interface.

Unfortunately you'll need to install the [CP210x USB to UART Bridge Virtual COM Port driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads) manually.

With the radio plugged in, _turned on_, and the drivers installed try listing your USB devices:

```
  ~% ioreg -p IOUSB

  [...]

  | +-o IOUSBHostDevice@02100000  <class IOUSBHostDevice, id 0x1000abb83, registered, matched, active, busy 0 (5243 ms), retain 30>
  |   +-o CP2105 Dual USB to UART Bridge Controller@02110000  <class IOUSBHostDevice, id 0x1000abb90, registered, matched, active, busy 0 (5218 ms), retain 28>
  |   +-o USB Audio CODEC @02120000  <class IOUSBHostDevice, id 0x1000abb9d, registered, matched, active, busy 0 (58 ms), retain 33>

  [...]

```

The ones to look for here are the `CP2105 Dual USB to UART Bridge Controller` and the `USB
Audio CODEC`.  If they are listed your computer can see the radio.  If not, try
pressing `menu` on the radio and confirm that option `037 CAT SELECT` is set to
`USB`.

Most of the radio's default options are fine, but there are a few to adjust:

- Set option `038 CAT RATE` to `38400` (default `4800`).
- Set option `075 DATA IN SELECT` to `USB` (default `DATA`)
- Set option `077 DATA OUT LEVEL` to `1` (default `50`)
- Set option `103 SSB MIC SEL` to `USB` (default `FRONT`).  Tip: Program your `C.S` key for this option so it's easy to switch back to the front microphone.

When using the radio for FT8 I also set these options:

- Set `IPO` to `IPO`
- Set `ATT` to `OFF`
- Set `PROC` to `OFF` (this option is behind the `SCOPE` button)
- Set `MIC EQ` to `OFF` (also behind the `SCOPE` button)

On OS X you'll need to install [WSJT-X](https://wsjt.sourceforge.io/wsjtx.html).  WSJT-X can control the radio directly so no need for any other software radios.  These are my settings:

![A screenshot of the radio tab of the WSJT-X settings window.]({{ site.baseurl }}/assets/img/2023-wsjt-x-settings.png)

I have two serial ports provided by the radio, one regular and one "enhanced" -
only the enhanced one works.
