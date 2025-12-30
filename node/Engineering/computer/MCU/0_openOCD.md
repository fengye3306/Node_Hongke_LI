OpenOCD（Open On-Chip Debugger）是一个开源的、支持多种芯片和调试器的片上调试工具。

传统芯片的调试方式，每个芯片都有自己的专用软件，同时每个调试器都有自己的驱动，配置复杂学习成本高。   
OpenOCD将其整合，使得统一接口支持多种调试器，灵活易用

```text
你的电脑   ←→  OpenOCD ←→ 调试器硬件   ←→ 目标芯片
(GDB/IDE)     (软件层)    (ST-LINK等)    (STM32等)
```

## OpenOCD启动指令

启动的核心目的是在调试器和目标芯片之间建立桥梁，提供三大调试服务（GDB、Telnet、TCL）, 三大服务细节后面会讲到。 

1. 初始化调试器（ST-LINK/CMSIS-DAP等）
2. 连接目标芯片（STM32/GD32等）
3. 启动调试服务，提供三大调试服务（GDB、Telnet、TCL）
4. 准备调试环境（复位芯片、设置断点等）


OpenOCD 指令 格式如`openocd -f <目标调试器配置> -f <目标芯片配置>  -c [选项]"`，由三个部分组成。  
其中例如，两个 `-f` 形参是固定输入,`-c` 选项形参是可以无限堆叠的选填


**最直观简洁的启动和目标类型芯片的链接，由环境中自动检索的目标调试器。指令启动三大调试服务**   
调试器类型与目标芯片支持均由开源社区更新维护，需要填写什么参数询问AI即可。  

```shell
# eg
openocd -f interface/stlink.cfg ^
        -f target/stm32f4x.cfg  ^
        -c "program firmware.elf erase verify reset"
```


### program（烧录程序）

命令行语法 `program <file> [address] [erase] [verify] [reset]`  

| 参数    | 说明                          |
|---------|-------------------------------|
| file    | ELF / BIN / HEX                 |
| address | 指定基地址，BIN 必须，ELF 不需要  |
| verify  | 写后校验                         |
| reset   | 烧录完成后复位                   |

```shell
# eg
-c "program firmware.elf erase verify reset"
-c "program firmware.bin 0x08000000 erase verify reset"
```

* ELF（Executable and Linkable Format） 文件，名为结构化可执行文件，文件特点在于**附带调试信息**，故而文件较大。  
文件本身可读，需要特殊工具解析，适用于调试环境。    
ELF 文件内部包含段地址（LMA / VMA），OpenOCD 在program xxx.elf 时将忽略命令行地址，完全按 ELF 内部地址烧录。  

* BIN（Binary File） 文件，名为纯二进制镜像文件，是**纯机器码文件**，故而**最小**。  
文件本身纯二进制，不可读，用于生产环境。其中，地址信息需要指定。    

*地址问题以STM32F407为例*   
0x00000000 - 0x07FFFFFF: 启动映射区（Alias）,0x00000000 并非真正的物理存储,启动时会根据 BOOT配置 映射到Flash 或者 SRAM ，或者System Memory
0x08000000 - 0x0807FFFF: Flash (512KB) 应用程序代码只应烧录到主Flash区  
0x20000000 - 0x2001FFFF: SRAM (128KB)   
0x40000000 - 0x5FFFFFFF: 外设  

所以对于STM32F407 系列单片机，其基地址为`0x08000000`,如果乱设定起始地址 烧录失败或程序跑飞崩溃。 面对不同的芯片型号查询即可。 






## 三个网络服务端口 

当OpenOCD启动后，它会同时开启**三个网络服务端口**，每个端口提供不同的功能：  




### GDB服务器  


### Telnet服务器

### TCL服务器  




## 指令  


## 适配器

OpenOCD 没有、也暂时不会提供“查询当前环境中已连接调试器”的统一指令；正确做法是在 OpenOCD 之前，用各厂商工具或系统 USB 枚举完成设备发现。

### ST-Link   

> STM32CubeProgrammer 下的ST-Link 查找

STM32CubeProgrammer（简称 STM32CubePROG）,这是 ST 官方为 STM32 微控制器提供的一体化编程工具。主要功能包括有：
* 擦除、编程、查看、验证 STM32 的 Flash 存储器
* 支持外部存储器（需自定义 Flash 加载器）

**安装**
1. 官方推荐（当前主流），使用 STM32CubeProgrammer  
安装地址：`https://www.st.com/en/development-tools/stm32cubeprog.html`  
2. 安装后添加默认路径进入path

**ST-LINK 设备查询** 

```shell
STM32_Programmer_CLI.exe -l
```
指令可以列出实际连接的物理设备，包括： `J-Link`,`STLink`,`UART`  







