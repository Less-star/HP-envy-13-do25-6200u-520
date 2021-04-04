--------[ 鲁大师 ]--------------------------------------------------------------------------------

  软件:             鲁大师 5.1021.1300.108
  时间:             2021-04-04 14:24:37
  网站:             http://www.ludashi.com

--------[ 概览 ]----------------------------------------------------------------------------------

  电脑型号            HP ENVY Notebook 笔记本电脑
  操作系统            Windows 10 专业版 64位 ( DirectX 12 )

  处理器              英特尔 Core i5-6200U @ 2.30GHz 双核
  主板                惠普 80DF ( 6th/7th Generation Intel Processor Family I/O - 9D48 笔记本芯片组 )
  主显卡              英特尔 HD Graphics 520 ( 128 MB / 惠普 )
  内存                8 GB ( SK Hynix LPDDR3 1600MHz )
  主硬盘              建兴 L8H-256V2G-HP ( 256 GB / 固态硬盘 )
  显示器              三星 SDC415A ( 13.3 英寸  )
  声卡                瑞昱  @ 英特尔 High Definition Audio 控制器
  网卡                英特尔 Wi-Fi 6 AX200 160MHz #2
-------[ 日志 ]----------------------------------------------------------------------------------

功能检测
   -----------Wi-Fi蓝牙；正常（隔空投送-英特尔网卡不支持）
   -----------声卡，显卡：正常
   -----------C P U变频：正常
   -----------S D读卡器：正常（休眠会炸，开启禁用s3可修复无睡眠）已禁用驱动
   -----------USB端口：已定制
   -----------键盘触控板手势：正常
   -----------鼠标仿白设置：需要自定义哦！
   -----------亮度调节，电量显示：正常
   -----------引导windos：正常
   -----------开机音：无法使用「具体原理上未搞清楚」
-------------------------------------------------------------上述检测信息实时更新，以最新版引导为校准------
更新

2020-12-10:  通过“https://opencore.slowgeek.com“构建OpenCore0.6.4正式版配置表设置参数
             并加载核心驱动+SSDT用于系统安装

核 心 驱 动：
         「 
             Lilu.kext                 =仿冒核心前置驱动
             VirtualSMC.kext           =虚拟SMC 
             AppleALC.kext             =声卡驱动 
             SMCProcessor.kext         =处理器驱动
             SMCSuperIO.kext           =IO传感器
             USBInjectAll.kext         =USB总线驱动
             WhateverGreen.kext        =图形卡驱动
             VoodooPS2Controller.kext  =笔记本键盘（触摸板）驱动
                                                                      」
核 心 补 丁：
         「
             SSDT-EC-USBX-LAPTOP       =仿冒并覆盖嵌入式控制器，并强制USB电源属性
                                                                             」
附 加 项 目：
             增加“CtlnaAHCIPort.kext”用于Big Sur系统下识别部分SATA磁盘（我的盘需要）。
             勾选惠普专用内核quirks选项“Lapic Kernel Panic”
             勾选SATA磁盘专用内核quirks选项“Third Party Drives”开启  TRIM支持
             完成上述，即可安装进系统了。
             设置六代笔记本推荐SMBIOS ：MacBookPro13,2及三码信息

主 板 设 置：  
             惠普这个机型主板设置相对简单，只需要关闭安全启动即可！！！


2020-12-11:  完善系统体验，设备硬件驱动完善。
             增加内核“Sinetek-rtsx.kext”      驱动内置SD卡读卡器。
             增加内核“BrightnessKeys.kext     驱动亮度调节
             增加内核“SMCBatteryManager.kext” 驱动电池电量显示
             增加内核“itlwm.kext"             驱动英特尔AX200Wi-Fi
             增加内核“HoRNDIS.kext“           驱动手机USB共享网络
             增加内核“USBPorts.kext”          定制USB端口信息
             增加内核“IntelBluetoothFirmware.kext”驱动英特尔蓝牙
             增加设备属性：显卡仿冒ID“AAPL,ig-platform-id=00001619”驱动显卡「并修补接口信息（这些不一定通用）」
             增加设备属性：声卡仿冒ID“layout-id=1C000000“驱动声卡（型号=ALC269/ID=28）
             增加ACPI补丁：“SSDT-PLUG.aml”开启节能五项
             增加ACPI补丁：“SSDT-PNLF.aml”驱动亮度调节快捷键

2021-01-09:  发现故障SD卡休眠无法识别，报错“您插入的磁盘在此电脑上不能读取”禁用S3睡眠后不再报错，但是耗电量增加。

2021-01-10:  升级OpenCore0.6.5正式版底包
             更换内核“itlwm.kext ”为「
                                      AirportItlwm_Big_Sur.kext
                                      AirportItlwm_Catalina.kext
                                      AirportItlwm_Mojave.kext
                                      AirportItlwm_High_Sierra.kext
                                                                      」修复各版本原生Wi-Fi开关使用
             增加驱动“CPUFriend.kext 与 CPUFriendDataProvider.kext“增强CPU变频管理
             增加内核“FakeAppleUSBMouse.kext”开启白果鼠标设置界面，开启更多鼠标自定义玩法（驱动需要自定义）

2021-01-20:  重新定义ssdt/Kexts注释名
             测试，检查，修复OC引导 Windows

2021-01-24:  升级OpenCore0.6.6正式版底包，更新个性图形化主题，增加图形化背景

2021-01-27:  移动Windows系统EFI文件至oc目录下用于BIOS默认启动项为oc
             添加MIsc自定义启动项绝对路径“\EFI\OC\Microsoft\BOOT\bootmgfw.efi”

2021-03-20:  升级OC0.6.7，调整部分驱动更新，完善休眠信息
             增加补丁：“SSDT-PMCR.aml”添加缺失设备，APP9876，NVRAM相关
             增加补丁：“SSDT-SBUS.aml“修复SBUS
             增加补丁：“SSDT-DWAK.aml“修复睡眠功能
             调整移动Windows系统EFI文件至oc目录下widows文件夹（让你更清楚知道这是什么文件夹）
             修改MIsc自定义启动项绝对路径“\EFI\OC\Windows\Microsoft\BOOT\bootmgfw.efi”

 分 享 修 改： 添加-v跑马模式，解除USB端口设置，移除内置网卡驱动，三码移除（弄好后自行更换新的）




