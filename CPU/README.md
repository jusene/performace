## CPU弹药库

1. sysstat工具集包

   - iostat 报告CPU统计及设备，分区和网络系统的输入/输出统计

     ```shell
     iostat
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     avg-cpu:  %user   %nice %system %iowait  %steal   %idle
               20.66    0.00    3.01    0.01    0.00   76.33
     
     Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s    kB_read    kB_wrtn    kB_dscd
     sda               3.72        28.68        94.72         0.00  547825382 1809096527          0
     磁盘名             每秒传输次数，一次传输一个I/O请求 每秒从设备读取的数据量 每次写入设备的数据量 
     ```

   - mpstat 报告单个或组合的处理器相关统计信息

     ```shell
     mpstat -P ALL
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:30:55 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
     11:30:55 AM  all   20.66    0.00    2.75    0.01    0.00    0.26    0.00    0.00    0.00   76.33
     11:30:55 AM    0   18.44    0.00    2.45    0.01    0.00    0.09    0.00    0.00    0.00   79.02
     11:30:55 AM    1   22.05    0.00    3.03    0.01    0.00    0.06    0.00    0.00    0.00   74.85
     11:30:55 AM    2   22.14    0.00    3.03    0.01    0.00    0.04    0.00    0.00    0.00   74.77
     11:30:55 AM    3   22.00    0.00    2.91    0.01    0.00    0.04    0.00    0.00    0.00   75.04
     11:30:55 AM    4   22.01    0.00    2.78    0.01    0.00    0.03    0.00    0.00    0.00   75.17
     11:30:55 AM    5   17.79    0.00    2.58    0.01    0.00    1.75    0.00    0.00    0.00   77.86
     11:30:55 AM    6   20.72    0.00    2.62    0.01    0.00    0.03    0.00    0.00    0.00   76.62
     11:30:55 AM    7   20.10    0.00    2.58    0.01    0.00    0.04    0.00    0.00    0.00   77.27
     ```

   - pidstat 报告Linux任务（进程）的统计信息：I/O,CPU.内存等

     ```shell
     pidstat  # 进程cpu使用率 
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:33:14 AM   UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
     11:33:14 AM     0         1    0.02    0.03    0.00    0.01    0.05     3  systemd
     11:33:14 AM     0         2    0.00    0.00    0.00    0.00    0.00     4  kthreadd
     11:33:14 AM     0         3    0.00    0.00    0.00    0.20    0.00     0  ksoftirqd/0
     
     pidstat -d # 进程io使用率
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:33:51 AM   UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s iodelay  Command
     11:33:51 AM     0         1      3.11     26.36      6.29    1004  systemd
     11:33:51 AM     0        63      0.00      0.00      0.00    8170  kswapd0
     11:33:51 AM     0       327      0.01      0.00      0.00    3968  xfsaild/sda1
     11:33:51 AM     0       400      0.00      0.00      0.00       5  systemd-journal
     
     pidstat -t # 线程cpu使用率
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:34:17 AM   UID      TGID       TID    %usr %system  %guest   %wait    %CPU   CPU  Command
     11:34:17 AM     0         1         -    0.02    0.03    0.00    0.01    0.05     2  systemd
     11:34:17 AM     0         -         1    0.02    0.02    0.00    0.01    0.04     2  |__systemd
     11:34:17 AM     0         2         -    0.00    0.00    0.00    0.00    0.00     4  kthreadd
     11:34:17 AM     0         -         2    0.00    0.00    0.00    0.00    0.00     4  |__kthreadd
     11:34:17 AM     0         3         -    0.00    0.00    0.00    0.20    0.00     0  ksoftirqd/0
     
     pidstat -w # 进程cpu上下文切换
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:35:44 AM   UID       PID   cswch/s nvcswch/s  Command
     11:35:44 AM     0         1      0.86      0.00  systemd
     11:35:44 AM     0         2      0.00      0.00  kthreadd
     11:35:44 AM     0         3      1.37      0.00  ksoftirqd/0
     
     pidstat -wt # 线程cpu上下文切换
     Linux 3.10.0-862.el7.x86_64 (jumpserver)        07/03/2020      _x86_64_        (8 CPU)
     
     11:36:04 AM   UID      TGID       TID   cswch/s nvcswch/s  Command
     11:36:04 AM     0         1         -      0.86      0.00  systemd
     11:36:04 AM     0         -         1      0.86      0.00  |__systemd
     11:36:04 AM     0         2         -      0.00      0.00  kthreadd
     11:36:04 AM     0         -         2      0.00      0.00  |__kthreadd
     11:36:04 AM     0         3         -      1.37      0.00  ksoftirqd/0
     11:36:04 AM     0         -         3      1.37      0.00  |__ksoftirqd/0
     
     ```

   - tapestat 报告连接到系统的磁带驱动器的统计信息

   - cifsiostat 报告CIFS统计信息

   - sysstat 只是sysstat配置文件的手册页，给出了sysstat命令使用的环境变量的含义

   - sar 收集，报告和保存系统活动信息（CPU，内存，磁盘，中断，网络接口，TTY，内核表等）

     ```shell
     sar -u 1 10 查看cpu
     sar -r 1 10 查看mem
     sar -n DEV 1 10 查看网络流量
     sar -d 1 10 
     ```

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

   ```shell
   top - 15:10:23 up 221 days,  5:13,  2 users,  load average: 0.47, 0.68, 0.96
   Tasks: 225 total,   1 running, 208 sleeping,   0 stopped,  16 zombie
   %Cpu(s):  2.8 us,  1.6 sy,  0.0 ni, 95.1 id,  0.0 wa,  0.0 hi,  0.5 si,  0.0 st
   KiB Mem : 16266496 total,  4665504 free,  3705640 used,  7895352 buff/cache
   KiB Swap: 16777212 total, 16777212 free,        0 used. 11519088 avail Mem
   
     PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
    1003 root      20   0  316392  86076  38276 S   7.0  0.5  15606:27 consul
   12169 root      20   0 1119292  68288  11172 S   6.6  0.4 123:28.96 python
    6404 root      20   0  901528  44188   4420 S   5.0  0.3  16868:07 python
   
   ```

4. perf 定位热点函数

   ```shell
   perf top -g
   perf record -g
   perf report
   
   ## 火焰图
   perf record -p 2322 -F 99 -g -e cpu-clock
   perf script -i perf.data &> perf.unfold
   git clone https://github.com/brendangregg/FlameGraph.git
   ./stackcollapse-perf.pl perf.unfold &> perf.folded
   
   
   ```

   

