# Brother Printer Firmware Update Tool

Script to update the firmware of some Brother printers (e.g. MFC).

## Idea:

Brother provides drivers etc. for Linux but when you want to update the firmware of your printer,
Brother only provides ugly programs for Windows or Mac OS.
I think, you should do firmware upgrades from time to time, because the supported printers have
advanced network functionality, like SNMP, HTTP Web Management UI, and much more.
Some of them can be connected with ethernet and some of them with WiFi.
The more features a system has, the greater is the risk of bugs.

You could try to use the official tools. You could try to run the Windows EXE in Wine for example.
First it seemed to work, but then it crashed - like almost always I tried to run programs in wine.
You could also extract the jar from the Mac OS DMG as described [here](https://avandorp.wordpress.com/2009/07/21/brother-printer-firmware-update-with-linux-brother-druckerfirmware-update-mit-linux/).
But unfortunately this tool didn't find my printer and I had no chance to debug the problems as it
didn't give me any hint, what it is trying to do.

Then I found blog posts like
[this](https://www.earth.li/~noodles/blog/2015/11/updating-hl3040cn-firmware.html), that described a
way to update the firmware with only standard Linux tools.
I tried it and it worked :tada:

To make it a bit easier, I wrote this simple script.

## What the script does:

1. Optional (if no IP is given): Discover the printer using MDNS
2. Get printer info (like model name, firmware versions, etc.) with SNMP
3. Query the firmware download URL from Brother API server
4. Download the firmware
5. Upload the firmware to the printer over port 9100 (PDL-Datastream / jetdirect)

## Tested with:

- MFC-9332CDW
- MFC-9142CDN
- DCP-9020CDW
- DCP-9022CDW
- HL-5370DW

## Usage

### A: Install package using pip:

```shell
pip install --user --upgrade brother-printer-fwupd
```

*If this does not work, try `pip install --user --upgrade brother_printer_fwupd`.*

### B: Development installation:

1. Clone the repo
2. Install system dependencies: `libxlt-dev`, `libxml2-dev`
3. `poetry install`
4. `poetry run brother_printer_fwupd.py`

Use at your own risk!™

Contributions welcome.

## License

[© 2021 sedrubal (GPLv3)](./LICENSE)
