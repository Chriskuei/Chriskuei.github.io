---
title: Enable HiDPI Mode in macOS
layout: post
description: Mimic a 2K Monitor as "Retina DIsplay" in Mac
---

macOS regards a 2k monitor as a TV, and is using the YCbCr color space rather than RGB. You need follow  instructions below if you want to enable HiDPI Mode in macOS.

### Requirements

- MacBook Pro
- a 2k monitor (e.g. AOC Q2790PQ)

### Disable SIP (System Integrity Protection)

- Restart Mac
- Hold down Command-R until you see an Apple icon and enter Recovery
- Select Terminal from the Utilities menu, then type

```bash
$ csrutil disable
```

- Restart

### Force RGB in macOS

- Download [patch-edid.rb](https://gist.github.com/adaugherity/7435890)

- Run patch-edid.rb in termimal. A new folder will be created in your home directory. You will find a file named 'DisplayProductID-xxxx'

- Open the file and edit like this

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
  <plist version="1.0">
  <dict>
    <key>DisplayProductName</key>
    <string>Q2790 - forced RGB mode (EDID override)</string>
    <key>IODisplayEDID</key>
    <data>AP///////wAF45AnZigAACUcAQSlPCJ4IkgVp1ZSnCcPUFS/7wDRwLMAlQCB
  gIFAgcABAQEBVl4AoKCgKVAwIDUAVVAhAAAeAAAA/QAyTB5jHgAKICAgICAg
  AAAA/ABRMjc5MAogICAgICAgAAAA/wBHUU5KOUhBMDEwMzQyAMg=
  </data>
    <key>DisplayVendorID</key>
    <integer>1507</integer>
    <key>DisplayProductID</key>
    <integer>10128</integer>
    <key>scale-resolutions</key>
    <array>
        <data>AAAKAAAABaAAAAABACAAAA==</data>
        <data>AAAFAAAAAtAAAAABACAAAA==</data>
        <data>AAAPAAAACHAAAAABACAAAA==</data>
        <data>AAAHgAAABDgAAAABACAAAA==</data>
        <data>AAAMgAAABwgAAAABACAAAA==</data>
        <data>AAAGQAAAA4QAAAABACAAAA==</data>
        <data>AAAKAgAABaAAAAABACAAAA==</data>
        <data>AAAKrAAABgAAAAABACAAAA==</data>
        <data>AAAFVgAAAwAAAAABACAAAA==</data>
    </array>
  </dict>
  </plist>
  
  ```

- You can also use the [tool](https://comsysto.github.io/Display-Override-PropertyList-File-Parser-and-Generator-with-HiDPI-Support-For-Scaled-Resolutions/) to generate scaled resolutions
- Save the file and move the entire directory into the '/System/Library/Displays/Contents/Resources/Overrides' folder
- Restart your computer

### Set resolution

- Download [RDM](https://github.com/avibrazil/RDM)

- \[Option] Turn on HighDPI

  ```bash
  $ sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true
  ```

  \[Option] Turn on font smoothing

  ```bash
  $ defaults -currentHost write -globalDomain AppleFontSmoothing -int 2
  # To undo it, try
  # defaults -currentHost delete -globalDomain AppleFontSmoothing
  ```

- Enable SIP

  ```bash
  $ csrutil enable
  ```

- Enjoy

### 

### References

\[1] [Force RGB mode in Mac OS X to fix the picture quality of an external monitor](https://www.mathewinkson.com/2013/03/force-rgb-mode-in-mac-os-x-to-fix-the-picture-quality-of-an-external-monitor)

\[2] [请教一下如何在 Mac OS X 10.11 下开启自定义 HiDPI？](https://www.zhihu.com/question/35300978)