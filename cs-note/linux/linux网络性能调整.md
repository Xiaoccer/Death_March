# 《Linux网络性能调整》

## 常用命令
* netstat -antp  //可以查看当前网络状态的连接情况
* ss -antmio  //与netstat类似，但还能查看连接使用内存的情况，使用的一些策略等
* sar -n  //Linux下系统运行状态统计工具
* ifconfig 
* route -n  // 查看路由表
* ip route show table all/ip rule show  //查看详细路由表
* tcpdump  //网络上的数据包进行截获的包分析工具
* nmap // 网络扫描和嗅探工具包
* tc //可设置网卡的一些规则
* slabtop //显示内核“slab”缓冲区的细节信息
* ulimit -a  //获取或设置每个进程的一些限制，如最大的文件描述符数等
* ls  /proc/1/fd -l  //查看Pid为1的文件描述符使用情况

## 性能调优
TCP性能调优：
* 调高带宽利用率，可将接收端的接收缓存和发送端的发送缓存增大为带宽时延积的大小。
* 若每次需要传输小文件时，可将tcp_slow_start_after_idle置为0，避免每次慢启动时的拥塞窗口过小。
* 若网络存在一定几率的掉包，则常用拥塞算法中的拥塞窗口会每次都减半，导致传输效率低下，可改用bbr拥塞算法。
网卡相关：
* 队列：rps rfs
* 协议：ufo tso
* dpdk、ebpf
其他：
* 置tcp_sysncookies为1，可以服务端存储半连接的空间。
