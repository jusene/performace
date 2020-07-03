## CPU弹药库

1. sysstat工具集包
   - iostat 报告CPU统计及设备，分区和网络系统的输入/输出统计
   - mpstat 报告单个或组合的处理器相关统计信息
   - pidstat 报告Linux任务（进程）的统计信息：I/O,CPU.内存等
   - tapestat 报告连接到系统的磁带驱动器的统计信息
   - cifsiostat 报告CIFS统计信息
   - sysstat 只是sysstat配置文件的手册页，给出了sysstat命令使用的环境变量的含义
   - sar 收集，报告和保存系统活动信息（CPU，内存，磁盘，中断，网络接口，TTY，内核表等）
   - sadc 是系统活动数据收集器，用作sar的后端
   - sa1 收集二进制数据并将其存储在系统活动每日数据文件中。它是可从cron或sytemd运行的sadc的前端
   - sa2 编写了一份总结的日常活动报告。它是可从cron或systemd运行sar的前端
   - sadf 以多种格式（CSV，XML，JSON等）显示sar收集的数据，并可用于与其他程序进行数据交换。此命令还可用于使用SVG（可缩放矢量图形）格式绘制sar收集的各种活动的图形。

2. vmstat 系统自带

   ```shell
   procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
    r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
    1  0 101548 133766984      8 125176048    0    0     0     4    0    0  0  0 100  0  0
    正在运行的进程 不可中断的进程 swap的容量 空闲内存的容量 buff内存容量 cache内存容量 从内存换入swap的io 从swap换出到内存的io 磁盘写入的io 磁盘读出的io 系统中断的次数 cpu上下文切换的次数 用户态cpu使用率 内核态cpu使用率 cpu空闲率 iowait cpu使用率 虚拟化cpu使用率
   ```

3. top 系统自带

   