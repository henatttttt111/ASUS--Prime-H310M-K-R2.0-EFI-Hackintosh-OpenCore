# ASUS--Prime-H310M-K-R2.0-EFI-Hackintosh-OpenCore
给华硕H310M-K R2.0打造的OpenCore，适配到macOS Sequoia，支持独显和核显


## 写在前头：

| | 系统和引导器版本 |
|-|---------|
| OpenCore | 1.0.7 Release |
| macOS | High Sierra - Sequoia（均测试过） |


## 我的配置

| 类别 | 型号| 备注 |
| ---------------------------- | ---------------------- |------------------|
| ``MB``| ASUS Prime H310M-K R2.0 | 400瓦电源 |
| ``CPU``| Intel Core i3-8100 3.6GHz |  |
| ``Memory``| 16GB DDR4-2400MHz | 金士顿 |
| ``iGPU``| Intel UHD Graphics 630 |  |
| ``dGPU``| AMD Radeon RX560 | 蓝宝石 |
| ``Wifi and Bluetooth``| Broadcom BCM943602CS | 白果卡，在14+需要用OCLP和我Test版本的EFI |
| ``Ethernet``| RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller | Use [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases). |
| ``Audio``| Realtek ALC887 | Add `alcid=11` to boot-arg or add layout-id to DeviceProperties. |

### 兼容的配置

|            硬件 | 型号                                                                                       | 
|---------------:|:-------------------------------------------------------------------------------------------|
|            主板 | 我估计华硕H310系列的主板都能支持                                                       |
|          处理器 | 8代和9代intel Core CPU，最好有核显                                           |
|           内存 | DDR4应该都行                                                                |
|           显卡 | 免驱卡应该都行  |
|     无线 + 蓝牙 | 博通白果卡和intel网卡                                       |
|           硬盘 | 这个机器只有SATA，SSD和Nvme应该都行                                       |
｜         显示器 ｜最好选支援HIDPI缩放的，配备DVI，HDMI或者DP的，核显VGA未测试                                 ｜


## 工作情况

| ``功能``|``情况``| 
|-------------|-----------|
| ``音频I/O``|✅|
| ``Wifi与Bluetooth``|✅|
| ``USB端口``|✅已经定制，速率正常|
| ``耳机端口``|✅|
| ``图形与加速``|✅|
| ``电源管理``|✅|                                                                        
| ``USB Port``|✅|
| ``iCloud 和 AppStore``|✅|
| ``Facetime和 iMessage``|✅|
| ``以太网``|✅|
| ``睡眠``|✅|
| ``DRM``|❗️纯的GPU正常，在dGPU+iGPU状态半正常，需终端执行代码，纯iGPU不正常，仅测试Apple Music和TV|

## 用前必看
本EFI分为**Realese**和**Test**两个版本
- **Release**可以在macOS13及之前的版本上使用，在这个版本中我们Secure Boot Model默认设置为x86legacy因此会破坏Big Sur之前版本的引导，如果你希望引导Catalina及之前的版本使用之前请把它改成Disabled。同时默认启用SIP。该版本不含对Sonoma后旧版博通WI-Fi框架的支持。
- **Test** 提供对Sonoma、Sequoia以及Tahoe的支持，则添加对Sonoma之后的macOS博通免驱Wi-Fi的支持，但安全性有所降低，且不支持增量更新。
- 添加了对iGPU的支持，如果你仅使用iGPU请删除#PciRoot(0x0)/Pci(0x2,0x0)前的并删掉PciRoot(0x0)/Pci(0x2,0x0)参数，和但是该主板仅有一个VGA接口和一个DVI接口，妥善考虑还是希望您选择DVI接口来输出视频画面，但是如果你非要使用VGA的话，本EFI提供了对VGA端口对支持未测试（DP的id和EDID，busID和con0和1的Type均注入」
- 添加OC的图形界面引导和Boot Chime开机音效。
- 使用OCAT等工具，为改EFI添加三码和ROM，SMIBIOS推荐设置为iMac19,2（iGPU与的GPU）、iMac Pro1,1 (仅有独显)、Mac mini8,1（仅有核显）

## 相关链接
- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [OpenCore Bootloader v0.8.0](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.8.0)
- [ProperTree](https://github.com/corpnewt/ProperTree)
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- [OCLP](https://github.com/dortania/OpenCore-Legacy-Patcher/releases)
- [OCAT](https://github.com/ic005k/OCAuxiliaryTools)
