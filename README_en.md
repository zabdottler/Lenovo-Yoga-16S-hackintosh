[简体中文](README.md)

# Lenovo-Yoga-16S-hackintosh

## Notes

**This EFI is for Monterey and Big Sur**

**Disable nootedred.kext in config.plist before install macOS**

**Have to disable one of the XHCI controller in this model, might not be necessary for your laptop**

**SMBIOS is deleted, you need to generate it by your own and fill in config.plist**

---
### Overview
![overview](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/总览.png)

---
### What's not working
1. Sleep

2. Internal mic

3. Randomly freeze, NVMe drive related?

4. No hardware encoding and decoding, you should install big sur if you need it 

### Spec

---
Components|Model|Compatibility
:-|:-|:-|
CPU|AMD Ryzen 7 5800H|☑️
iGPU|AMD Radeon Vega 8 (Renoir)|☑️
dGPU|Nvidia RTX 3050laptop|✖️
Network card|Intel AX200|☑️，original MTK7921✖️
Drive|SAMSUNG PM9A1|☑️，original PM981A✖️
Trackpad|I2C HID|☑️
Keyboard|PS2 controller|☑️
Touch Screen|I2C ELAN|☑️
Bluetooth|Intel AX200|☑️，original MTK7921✖️
HDMI output||☑️
Audio/3.5mm jack|ALC287|☑️
Ram|Mircon DDR4 3200MHz|☑️
USB|by disabling XCHI0|☑️

---
## Know your EFI

---
### ACPI
SSDT | What for
:---------|:---------
SSDT-PLUG-ALT | Fixes CPU definitions
SSDT-EC | Adds a fake Embedded Controller device
SSDT-HPET | Fixes IRQ conflicts
SSDT-SBUS-MCHC | Fixes AppleSMBus
SSDT-USBX | Enables USB Power Management
SSDT-XOSI | Spoof macOS to Windows for some ACPI features.
SSDT-ALS0 | NootedRed provided, for brightness control
SSDT-PNLF | NootedRed provided, for brightness control

---
### Kexts
Kext | What for
:---------|:---------
AMDRyzenCPUPowerManagement | AMD CPU power management
AppleALC | fixed audio
AppleMCEReporterDisabler | Disables AppleIntelMCEReporter which causes panics on AMD CPUs
ECEnabler | Battery reading fixes
Lilu | Patch Engine
NVMeFix | NVMe Power Management
RestrictEvents | Change CPU Name
SMCAMDProcessor | Companion to AMDRyzenCPUPowerManagement
SMCBatteryManager | Battery reading
USBToolBox | USBmap tool
USBMapLegacy.kext | USBmap, you need generate your own if not the same model
VirtualSMC | Advanced Apple SMC emulator in the kernel
VoodooPS2Controller | PS/2 keyboard，need to disable voodoops2 input as it will conflict with i2c's input in config.plist
NootedRed | Enable AMD iGPU acceleration
NullEthernet | Enable iCloud login on laptops with no ethernet port
VoodooI2C | Trackpad/Touch Screen
VoodooI2CHID | Trackpad/Touch Screen
BrightnessKeys | Enable brightness controll key on keyboard
AirportItlwm | Enable Intel AX200 wifi
BlueToolFixup | Enable bluetooth on Montery with IntelBluetoothFirmware
IntelBluetoothFirmware | Enable bluetooth. 
IntelBluetoothInjector | Enable bluetooth on Big Sur with IntelBluetoothFirmware
IntelBTPatcher | Enable bluetooth on Big Sur with IntelBluetoothFirmware

Intel Bluetooth combo: 

Monterey: IntelBluetoothFirmware+BlueToolFixup

Big sur: IntelBluetoothFirmware+IntelBluetoothInjector+IntelBTPatcher

---
### USB

---
Disable one of the XHCI controller via UMAF，see how-to https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

There are 2 XHCI controllers in Yoga 16S(Slim pro 7): XHCI0 is controlling 1 USB-A port,the one next to power button;XHCI1 controls everythin else includeing USB-C/USB-A/Bluetooth/Front cam.

you better disable XHCI0.

---
### Thermals
You can disable Core Performance Boost via UMAF or AMD Power Gadget to get lower temperature and lower CPU performence. 

---
### Credits

---
Thanks for devs of NootedRed，making AMD iGPU hackintosh possible
>https://github.com/NootInc/NootedRed

And guides from EtremeXT
>https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

---
### Screenshots
![display setting](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/显示器设置.png)
![multi-screen](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/多屏幕.png)
![wifi](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/Wi-Fi设置.png)
![bluetooth](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/蓝牙设置.png)
![geekbench with cps disable](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/开启cps的跑分.png)
