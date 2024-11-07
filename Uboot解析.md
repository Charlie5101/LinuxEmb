# Uboot解析
## uboot源码结构

| 目录/文件 | 说明                  |
| :-------- | --------------------- |
| api       | 通用的API函数相关目录 |
| arch      | 与芯片架构相关目录    |
| board     | 板级相关信息目录      |
| cmd       | uboot命令相关目录     |
| common    | 通用代码目录          |
| configs   | boot配置文件目录      |
| disk      | 磁盘相关内容目录      |
| doc       | 说明文档              |
| drivers   | 驱动代码相关目录      |
| dtoverlay |                       |
| dts       | 设备树相关目录        |
| env       | uboot环境相关         |
| examples  | 示例代码目录          |
| fs        | 文件系统相关目录      |
| include   | 头文件相关目录        |
| lib       | lib库文件目录         |
| Licenses  | 许可证相关目录        |
| net       | 网络相关代码目录      |
| post      | 上电自检相关目录      |
| scripts   | 相关脚本目录          |
| test      | 测试代码目录          |
| tools     | uboot构建工具相关目录 |
| Kconfig   | 图形配置界面相关文件  |
| Makefile  | Makefile文件          |

## 图形化配置解析
​	**\> Architecture select (ARM architecture)  ---\>  处理器架构选择**
​	\>
​	**\> ARM architecture  ---\> ARM 架构子选项**
​		\>[ ] Support for ARM SMC Calling Convention (SMCCC) 支持SMCCC,这是一个开源的Minecraft启动器核心库,SMCCC介绍点击打开链接
​		\>[ ] support boot from semihosting     支持半主控，用于调试
​		\>[\*] Build U-Boot using the Thumb instruction set    用thumb指令建立uboot
​		\>[\*] Build SPL using the Thumb instruction set    用thumb指令建立SPL
​		\>[ ] L2cache off 
​		\>[\*] Use an assembly optimized implementation of memcpy    memcpy用汇编优化执行
​		\>
​		\>[ ] ARM64 system support AArch32 execution state  32位执行支持
​		\>    Target select (Samsung EXYNOS)  ---\> 目标芯片选择
​		\>[ ] EXYNOS architecture type select 
​		\>[ ] Use LPAE page table format    页表格式
​		\>[ ] Support the \'dek_blob\' command
​		\>    ARM debug  ---\>    调试
​	**\>  General setup  ---\>**
​		\>()  Local version - append to U-Boot release    版本号
​		\>[\*] Automatically append version information to the version strin
​		\>[\*] Optimize for size  优化大小
​		\>[\*] Select defaults suitable for booting general purpose Linux di│    选择何时的启动
​		\>[\*] Enable malloc() pool before relocation   使能malloc池在引导之前
​		\>(0x400) Size of malloc() pool before relocation    malloc大小
​		\>[\*] Configure standard U-Boot features (expert users)  ---\>    配置标准的uboot特性
​		\>[ ] 64bit physical address support     64位物理地址支持
​	**\>    Boot images  ---\>    镜像**
​		\>[\*] Enable support for Android Boot Images    使能安卓引导
​		\>[\*] Support Flattened Image Tree 支持扁平镜像树
​		\>[\*]   Support SHA256 checksum of FIT image contents     支持FIT镜像校验和
​		\>[ ]   Enable signature verification of FIT uImages    FIT uimage签名验证
​		\>[ ]   Show verbose messages when FIT images fail    打印信息当FIT镜像失败
​		\> [ ]   Select the best match for the kernel device tree    选择最好的匹配到设备树
​		\>-\*-   Support Flattened Image Tree within SPL
​		\>[ ]   Enable signature verification of FIT firmware within SPL 
​		\>[\*]   Enable SPL loading U-Boot as a FIT
​		\>[ ] Set up board-specific details in device tree before boot
​		>
​	**\> API  --->**
​		\>[ ] Enable U-Boot API 使能uboot api
​	**\>    Boot timing  --->  开机时序**
​		\>[ ] Boot timing and reporting     开机报告
​		\>(20) Number of boot ID numbers available for user use    引导ID给 user
​		\>(30) Number of boot stage records to store    引导记录数
​		\>(0) Address to stash boot timing information     开机时序记录存储地址
​		\>(0x1000) Size of boot timing stash region     存储区大小
​	**\>Boot media  ---> 引导媒介**
​		\>
​	**\>(2) delay in seconds before automatically booting     自动引导延时**
​	**\>[ ] Enable boot arguments 启动参数**
​		\>()    Boot arguments 
​	**\>    Console  --->  控制台**
​		\>[ ] Console recording  控制台记录
​		\>()  Board specific string to be added to uboot version string
​		\>[ ] Support a silent console 支持无信息控制台
​		\>[ ] Buffer characters before the console is available    控制台之前有效字符缓冲
​		\>[ ] Enable console multiplexing    使能控制台复用
​		\>[ ] Select console devices from the environment      选择控制台设备根据环境
​		\>[ ] Allow board control over console overwriting    允许控制台覆盖板控制
​		\>[ ] Update environment variables during console init   更新环境变量在控制台初始化之前
​		\>[\*] Don't display the console devices on boot    在boot里面不显示控制台设备
​		\>[ ] Allow deregistering stdio devices     允许注销输入输出设备
​	**\>[ ] Support a FIT image embedded in the U-boot image  支持FIT镜像到U-boot镜像点击打开链接
​	\>()  Default fdt file 默认的fdt文件
​	\>[\*] add U-Boot environment variable vers    增加环境矢量
​	\>[\*] Display information about the CPU during start up    启动显示CPU信息
​	\>[\*] Display information about the board during start up    启动显示板子信息
​	\>    Start-up hooks  ---> 启动钩子函数
​	\> Security support  ---- 安全支持
​	\>    SPL / TPL  ---> SPL是uboot第一阶段执行的代码. 主要负责搬移uboot第二阶段的代码到内存中运行.SPL是由固化在芯片内部的ROM引导的. 我们知道很多芯片厂商固化的ROM支持从nandflash, SDCARD等外部介质启动**
​	**\>    Command line interface  ---> 命令行接口**
​		\> [\*] Support U-Boot commands
​		\>    Autoboot options  ---> 自动引导选项
​		\>
​		\>[\*] Fastboot support  ---> fastboot支持，fastboot是一种比recovery更底层的刷机模式
​		\>
​		\>   Info commands  ---> 
​		\>   Boot commands  ---> 启动命令
​		\> Environment commands  --->    环境命令
​		\>
​		\>   Memory commands  --->    内存命令
​		\>   Compression commands  ---> 压缩命令
​		\>   Device access commands  ---> 设备控制命令
​		\>  Shell scripting commands  ---> 脚本命令
​		\>  Network commands  --->    网络命令
​		\>   Misc commands  --->    函数命令
​		\> Power commands  ----    电源控制命令
​		\>   Security commands  --->    安全命令
​		\> Firmware commands  ----      固件命令
​		\>   Filesystem commands  --->     文件系统命令
​		\>  Debug commands  --->       调试命令
​		\>[ ] Enable UBI - Unsorted block images commands    是一种用于Raw Flash的卷管理系统，主要功能是在同一个Flash芯片上管理多个逻辑卷，并且平衡整个Flash读写操作
​	**\> Partition Types  ---> 分区类型
​	\>
​	\>   Device Tree Control  ---> 设备树控制
​	\>
​	\>   Environment  --->    环境
​	\>
​	\>-\*- Networking support  ---> 网络支持
​	\>
​	\>    Device Drivers  --->    设备驱动
​	\>
​	\>   File systems  ---> 文件系统
​	\>    Library routines  --->    库程序
​	\> [ ] Unit tests  ----    单元测试**

## 启动流程分析