
## 内核隔离

从内核调度器中讲指定的cpu排除，避免普通进程被调度到被隔离的cpu上运行。   
被隔离的cpu通常被用于特殊用途，通常是实时任务（低延迟需求）。    
      
## debian内核隔离实现

`isolcpus`参数的配置可以隔离特定cpu核心，参数将被添加至**GRUB**行中。  

> GRUB

GRUB 是一个用于加载和管理系统启动的完整程序。它是 Linux 发行版中最常见的引导程序(bootloader)。引导程序是计算机启动时运行的第一个软件。它加载 操作系统的内核，然后再由内核初始化操作系统的其他部分（包括 Shell、显示管理器、桌面环境 等等）。  

> 隔离内核并设置为实时核

本质是编辑GRUB配置文件，文件位于 `/etc/default/grub`  
打开此文件可以发现顶部注释：如果你修改了此文件，则保存后运行`update-grub`指令以修改`boot/grub/grub.cfg`  
即，`grub.cfg`是实际的脚本，脚本是通过配置文件所生成。  

目标是使得进行内核隔离。  
1. CPU内核标号是从0开始的，例如如果是四核心则0,1,2,3
2. 不要隔离所有CPU，至少保留CPU 0给系统进程 
3. 运行`sudo update-grub`使得修改生效
4. 修改GRUB配置后必须重启才能生效  
 
使得修改`isolcpus`，将通过修改`GRUB_CMDLINE_LINUX_DEFAULT`条目，条目用于GRUB配置文件中用于设置默认内核启动参数的变量。  

通常，默认安装debian os配置如下`GRUB_CMDLINE_LINUX_DEFAULT="quiet"`,参数配置可以如下。
```ssh
# 显示相关
"quiet"          # 安静模式，减少启动时的日志输出
"splash"         # 显示启动动画/画面
"nosplash"       # 不显示启动画面

# 图形相关
"nomodeset"         # 禁用内核模式设置（解决显卡问题）
"i915.modeset=0"    # 禁用Intel显卡模式设置
"radeon.modeset=0"  # 禁用AMD显卡模式设置

# 性能/调试
"isolcpus=1-3"   # CPU隔离
"nohz_full=1-3"  # 无时钟滴答模式
"console=ttyS0"  # 串口控制台
"debug"          # 启用调试信息
```

这次仅仅添加内核隔离可以修改为例如，`GRUB_CMDLINE_LINUX_DEFAULT="quiet isolcpus=7"`
语法`isolcpus=7`表示隔离第八个核心，`isolcpus=4-7`这个语法表示隔离5-8个核心。 这是隔离内核。  



如果要提高内核的实时性 则还有更新方案使得设置 `nohz_full`启动参数和 `rcu_nocbs`启动参数。  

`nohz_full`即无时钟滴答，Tickless模式。普通CPU每一秒存在1000次时钟中断，每次中断会打断正在运行的任务，造成延迟与不稳定性。使用 nohz_full 的CPU大部分时间没有时钟中断只有在真正需要时才响应更适合实时任务。  
`rcu_nocbs`用于在指定的CPU核心上禁用RCU（Read-Copy-Update）回调处理，RCU（读-复制-更新）：Linux内核的一种同步机制，用于安全地共享数据，避免锁竞争。但RCU回调会产生中断，影响实时性  

两者都有巨大风险，工业场景追求稳定性不必如此。  
`GRUB_CMDLINE_LINUX_DEFAULT="quiet isolcpus=4-7 nohz_full=4-7 rcu_nocbs=4-7"`





> 验证内核隔离

* `cat /sys/devices/system/cpu/isolated` 查看哪些CPU被隔离了




