[English](README_en.md)

# Lenovo-Yoga-16S-hackintosh

## 说明

**本EFI仅供Big Sur至Sonoma使用**

**在安装MacOS完成前请在config.plist中禁用nootedred.kext**

**本机型需要关闭一个XCHI控制器，不然会卡-V**

**机型信息已删除，请自行生成更换**

**OpneCore版本0.9.2 release（Big Sur-Ventura）/ 0.9.3 debug（Sonoma）**

---
## 总览
![overview](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/关于本机.png)
![overview](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh/raw/main/图片:Images/Lockscreen.jpeg)

---
### 存在的问题
1.睡眠

2.内置麦克风

3.偶尔卡住，主要表现在刚开机或者某些需要硬件加速的情况

4.VCN（硬件编解码）暂时还有问题，具体请移至NootedRed页面查看最新进展

5.WIFI目前只能使用itlwm搭配heliport软件进行使用，需要开机启动的可以编辑itlwm.kext里面的info.plist将你需要开机就连接的WiFi信息注入，具体参考https://openintelwireless.github.io/itlwm/FAQ.html

6.无法使用隔空投送等功能（Sonoma）
### 配置

---
部件|型号|是否支持
:-|:-|:-|
CPU|AMD Ryzen 7 5800H|支持
核显|AMD Radeon Vega 8 (Renoir)|支持
独立显卡|Nvidia RTX 3050laptop|不支持
网卡|Intel AX200|支持，原装MTK7921不支持
硬盘|三星PM981A|不支持，更换PM9A1解决
触控屏|I2C HID|支持
键盘|PS2 controller|支持
触控屏|I2C ELAN|支持
蓝牙|Intel AX200|支持，原装MTK7921不支持
HDMI输出||支持
音频/3.5耳机接口|ALC257|支持
内存|镁光DDR4 3200MHz|支持
USB|关闭XCHI0|支持

---
## 了解你的EFI

---
### ACPI
SSDT | 作用
:---------|:---------
SSDT-PLUG-ALT | 用于MacOS识别CPU，必须
SSDT-EC | 欺骗MacOS的假EC，必须
SSDT-HPET | 解决IRQ冲突，必须
SSDT-SBUS-MCHC | 解决AppleSMBus
SSDT-USBX | USB电源管理，必须
SSDT-XOSI | MAC和WIN的ACPI功能，双系统必须
SSDT-ALS0 | NootedRed提供，用于屏幕亮度调整
SSDT-PNLF | NootedRed提供，用于屏幕亮度调整

---
### Kexts
Kext | 作用
:---------|:---------
AMDRyzenCPUPowerManagement | AMD CPU 电源管理
AppleALC | 音频驱动
AppleMCEReporterDisabler | 关闭AppleIntelMCEReporter，避免在AMD CPU的设备上报错
ECEnabler | 电池读取
Lilu | 必备
NVMeFix | NVMe硬盘电源管理
RestrictEvents | CPU改名
SMCAMDProcessor | AMDRyzenCPUPowerManagement的附属
SMCBatteryManager | 电池管理
USBToolBox | USB定制
USBMapLegacy.kext | USB定制，这里我用的是legacy方式，限定了这个USB定制是在MacBookPro16,3机型使用，需要自行定制
VirtualSMC | 必备
VoodooPS2Controller | PS/2 键盘，需要在config中禁用voodoops2 input以避免与i2c的input冲突，不影响使用
NootedRed | AMD核显驱动
NullEthernet | 使无网口设备在MacOS可以登录iCloud
VoodooI2C | 触控板或触屏驱动
VoodooI2CHID | 触控板或触屏驱动
BrightnessKeys | 亮度调节按键
AirportItlwm | 英特尔网卡驱动，注意不同的系统有不同的kext
BlueToolFixup | 蓝牙驱动，Monterey中搭配IntelBluetoothFirmware使用
IntelBluetoothFirmware | 蓝牙驱动
IntelBluetoothInjector | 蓝牙驱动,在Big Sur中搭配IntelBluetoothFirmware使用
IntelBTPatcher | 蓝牙驱动,在Big Sur中搭配IntelBluetoothFirmware使用
itlwm | 英特尔WiFi驱动，需要安装heliport软件搭配使用，ax200测试可以在Sonoma beta1中使用

英特尔网卡的蓝牙驱动组合: 
Sonoma: 暂无蓝牙需求所以未测试

Monterey/Ventura: IntelBluetoothFirmware+BlueToolFixup+IntelBluetoothFirmware

Big sur: IntelBluetoothFirmware+IntelBluetoothInjector+IntelBTPatcher

---
### 关于USB

---
使用UMAF工具进入高阶bios对设备的XCHI控制器进行禁用，具体参考https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

在本机型中，存在两个XCHI控制器，XCHI0是电源键旁边那个USB-A口；XCHI1则是剩下的USB-A和USB-C，以及摄像头和网卡都由XCHI1控制，建议关闭XCHI0

---
### 温度
可以通过关闭CPS(core performence boost）将温度控制在比较合适的范围，但是会损失一部分性能。可以通过UMAF在bios中关闭CPS，但是会影响其他系统比如windows的性能，建议是每次开机进系统后通过AMD Power Gadget关闭，至少目前是只能这样。

---
### 致谢

---
感谢NootedRed的开发者们，使得AMD核显黑苹果成为可能
>https://github.com/NootInc/NootedRed

以及ExtremeXT的教程和指导
>https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

---
