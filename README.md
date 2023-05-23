# Lenovo-Yoga-16S-hackintosh

## 说明

**本EFI仅供Monterey即MacOS 12使用**

**在安装MacOS前请在config.plist中禁用nootedred.kext**

**本机型需要关闭一个XCHI控制器，不然会卡-V**

**机型信息已删除，请自行生成更换**

### 配置

---
部件|型号|是否支持
:-|:-|:-|
CPU|AMD Ryzen 7 5800H|支持
核显|AMD Radeon Vega 8 (Renoir)|支持
独立显卡|Nvidia RTX 3050laptop|不支持
网卡|MTK7921|不支持
硬盘|三星PM981A|不支持，更换PM9A1解决
触控屏|I2C HID|支持
键盘|PS2 controller|支持
触控屏|I2C ELAN|支持
蓝牙|MTK7921|不支持
HDMI输出||支持
音频/3.5耳机接口|ALC287|支持
内存|镁光DDR4 3200MHz|支持
USB|关闭XCHI0|支持

---
###关于USB

---
使用UMAF工具进入高阶bios对设备的XCHI控制器进行禁用，具体参考https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

在本机型中，存在两个XCHI控制器，XCHI0是电源键旁边那个USB-A口；XCHI1则是剩下的USB-A和USB-C，以及摄像头和网卡都由XCHI1控制，建议关闭XCHI0

---
###致谢

---
感谢NootedRed的开发者们，使得AMD核显黑苹果成为可能
>https://github.com/NootInc/NootedRed

以及ExtremeXT的教程和指导
>https://github.com/ExtremeXT/Lenovo_Legion_5_Hackintosh

