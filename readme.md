基本信息
-

* 适配机型：Acer Aspire V5-473G／573G
* 仿冒机型：MacBookPro11,2<sup>1</sup>
* CPU：Intel Core i5-4200U<sup>2</sup>
* GPU：Intel HD Graphics 4400<sup>3</sup> + NVIDIA Geforce GT750M<sup>4</sup>
* SSD：SanDisk SDSSDXPS480G
* 无线网卡：Fenvi BCM94352HMB<sup>5</sup>
* 有线网卡：RealtekRTL8111
* 系统版本：macOS Sierra 10.12.1 (16B2657)
* Clover 版本：3923

注意事项
-

### 系统安装
1. 进行安装系统前，请先在 Clover 启动选项中 **取消 Intel 集显的注入** 再进入系统安装盘，否则会遇到花屏。<sup>6</sup>
2. 安装完系统后，为使 kexts 生效，请进入 Recovery HD，在终端中输入命令：`csrutil disable`以关闭 SIP，然后重启。也可使用其他方法关闭 SIP。
3. 建议自行计算 SMBIOS 中的 **Serial Number**、 **SmUUID** 以及 **Board Serial Number** 注入到 config.plist，以配合 iMessage 与 FaceTime 等功能。[点击查看操作方法](http://bbs.pcbeta.com/viewthread-1679216-1-1.html)

### 关于仿冒机型的选择
常见的仿冒机型为 **MacBookAir6,2**，这里则建议使用的仿冒机型为 **MacBookPro11,2** 或以上。<br><br>
虽然 **MacBookAir6,2** 或 **MacBookPro11,1** 从配置角度而言更接近于我们的机型，但使用这些仿冒机型时，变频策略过于倾向节能，不仅 CPU 在常温下便主动降频，GPU 默认频率也过低，容易出现掉帧卡顿，性能表现与 Windows 10 下产生一定的差异。<br><br>
若仿冒 **MacBookAir7,2** 和 **MacBookPro12,1** 等采用 Broadwell 处理器的型号时，则变频档位不完全，失去低频档位。<br><br>
经测试，仿冒 **MacBookPro11,2** 时，变频档位完全，且主频能较好的维持在 1.6 GHz以上。实际使用中，性能与节能兼顾，续航依旧不错。


    以上的结果均在加入 SSDT 变频补丁的情况下测得。

### 关于双系统
双系统的实现方法有很多，这里不准备赘述。但为了正常体验双系统，建议阅读以下两篇教程：
* [解决双系统时间同步问题](http://bbs.pcbeta.com/viewthread-1692150-1-1.html)
* [解决双系统蓝牙鼠标共用问题](http://bbs.pcbeta.com/viewthread-1034129-1-1.html)

### 关于独显屏蔽
1. 开机按 **F2** 进入 BIOS 界面，按下 **Tab** 和 **Fn** 组合键，接着按 **Ctrl** + **Alt** + **Del** 组合键重启。
2. 在开机画面按 **F2** 以再次进入 BIOS 界面，此时 *Advanced* 和 *Power* 两个高级选项卡开启了。
3. 进入 *Advanced* 选项卡，在 *Video Configuration* 中将显卡模式由 **SG** 改为 **IGFX** ，然后将 *PCI Express Graphic* 改为 **Disable**。
4. 按 **F10** 保存 BIOS 设置，退出。


    使用 BIOS 屏蔽独显是简单粗暴的方法，既容易操作又不会出错。大多数 473G／573G 用户选择 DSDT&SSDT 屏蔽独显以方便在 Windows 下继续使用独显，[点击查看操作方法](https://github.com/Kaijun/Acer-V5-573g-DSDT)

### 存在的问题
1. 因使用 **ApplePS2SmartTouchPad.kext** 以支持多指触控手势，**Fn** 组合键功能受限，尚未实现快捷键调节亮度的功能。或许可以通过 DSDT 补丁实现。<sup>7</sup>
2. 同样因使用 **ApplePS2SmartTouchPad.kext**，触摸板设置页面显示为空白，需使用 El Capitan 的选项文件替换。<sup>8</sup>
3. 在切换 *机身内置麦克风* 和 *3.5mm 耳麦* 时不灵敏，比如：不能立即识别插入的 EarPods 的麦克风，或拔出 EarPods 后无法立即切换到内置麦克风。同时，目前暂未能支持 EarPods 按钮的线控，未来或将通过定制 **AppleALC.kext** 解决问题。<sup>9</sup>

<sup>1</sup>	仿冒机型的选择请自便

<sup>2</sup>	其他 CPU 型号需要自行更换对应的 SSDT 补丁以实现完美变频

<sup>3</sup>	注入为 0x0a16000c

<sup>4</sup>	需通过 BIOS 禁用，禁用方法见[关于独显屏蔽](###关于独显屏蔽)

<sup>5</sup>	原装网卡 Wi-Fi 功能无解，有需要建议更换为该型号

<sup>6</sup>	此处的操作是临时的，下次启动不会生效

<sup>7</sup>	若介意该功能缺陷，但不介意缺少多指手势，可更换为 VoodooPS2controller.kext

<sup>8</sup>	所需文件已放置在 etc 文件夹，请自行替换到系统目录下：/System/Library/PreferencePanes

<sup>9</sup>	声卡 ID 在 clover 中注入为 86，不需耳麦功能者，建议改为 3 会更为稳定
