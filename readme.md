# 适配机型：Acer Aspire V5-473G／573G
- 仿冒机型：MacBookPro11,2
- CPU：Intel Core i5-4200U
- GPU：Intel HD Graphics 4400 + NVIDIA Geforce GT750M（BIOS禁用，禁用方法见下文）
- SSD：SanDisk SDSSDXPS480G
- 无线网卡：Fenvi BCM94352HMB（原装卡无解，自行更换）
- 有线网卡：RealtekRTL8111
- 系统版本：macOS Sierra 10.12.1 (16B2657)
- Clover 版本：3923

---- 
# 文件内容
1. Clover 3923（config.plist 配置完毕）
2. DSDT 及 SSDT 补丁
3. Sierra 所需 kext 补丁

---- 
# 注意事项

## 存在的问题
1. 我使用 **ApplePS2SmartTouchPad.kext** 以支持多指触控手势，因此 **Fn** 组合键功能受限，尚未实现快捷键调节亮度的功能。
2. 系统选项中触摸板选项为空白，需使用 El Capitan 的选项文件替换。

## 系统安装
1. 进行安装系统前，请先在 Clover 启动选项中 **取消 Intel 集显的注入** 再进入系统安装盘，否则会遇到花屏。
2. 安装完系统后，为使 kexts 生效，请进入 Recovery HD，在终端中输入命令：`csrutil disable`以关闭 SIP，然后重启。也可使用其他方法关闭 SIP。
3. 建议自行计算 SMBIOS 中的 **Serial Number**、 **SmUUID** 以及 **Board Serial Number** 注入到 config.plist，以配合 iMessage 与 FaceTime 等功能。[点击查看操作方法][1]

## 关于仿冒机型的选择
- 常见的仿冒机型为 **MacBook Air6,2**，这里则建议使用的仿冒机型为 **MacBookPro 11,2** 或以上。
- 虽然 **MacBook Air6,2** 或 **MacBook Pro11,1** 从配置角度而言更接近于我们的机型，但使用这些仿冒机型时，变频策略过于倾向节能，不仅 CPU 在常温下便主动降频，GPU 默认频率也过低，容易出现掉帧卡顿，性能表现与 Windows 10 下产生一定的差异。
- 若仿冒 **MacBook Air7,2** 和 **MacBook Pro12,1** 等采用 Broadwell 处理器的型号时，则变频档位不完全，失去低频档位。
- 经测试，仿冒 **MacBook Pro11,2** 时，变频档位完全，且主频能较好的维持在 1.6 GHz以上。实际使用中，性能与节能兼顾，续航依旧不错。
*以上的结果均在加入 SSDT 变频补丁的情况下测得。*

## 关于双系统
双系统的实现方法有很多，这里不准备赘述。但为了正常体验双系统，建议阅读以下两篇教程：
- [解决双系统时间同步问题][2]
- [解决双系统蓝牙鼠标共用问题][3]

## 关于独显屏蔽
1. 开机按 **F2** 进入 BIOS 界面，按下 **Tab** 和 **Fn** 组合键，接着按 **Ctrl** + **Alt** + **Del** 组合键重启。
2. 在开机画面按 **F2** 以再次进入 BIOS 界面，此时 *Advanced* 和 *Power* 两个高级选项卡开启了。
3. 进入 *Advanced* 选项卡，在 *Video Configuration* 中将显卡模式由 **SG** 改为 **IGFX** ，然后将 *PCI Express Graphic* 改为 **Disable**。
4. 按 **F10** 保存 BIOS 设置，退出。

[1]:	http://bbs.pcbeta.com/viewthread-1679216-1-1.html "[教程] 无白果三码解决iMessage FaceTime牛逼方法整理"
[2]:	http://bbs.pcbeta.com/viewthread-1692150-1-1.html "[分享] 时间同步补丁Windows版"
[3]:	http://bbs.pcbeta.com/viewthread-1034129-1-1.html "[教程] 解决Windows 与Mac 双系统下的蓝牙设备共用的问题"