itle: Linux iostat io 性能查看
  - Ubuntu
categories:
  - Ubuntu
date: 2020-07-01 10:00:00
---
## 1、安装
```shell
apt install sysstat
```

## 2、命令说明
#### iostat[参数][时间][次数]
#### 通过iostat方便查看CPU、网卡、tty设备、磁盘、CD-ROM 等等设备的活动情况,负载信息。

## 3、命令参数
```shell
-C 显示CPU使用情况
-d 显示磁盘使用情况
-k 以 KB 为单位显示
-m 以 M 为单位显示
-N 显示磁盘阵列(LVM) 信息
-n 显示NFS 使用情况
-p[磁盘] 显示磁盘和分区的情况
-t 显示终端和CPU的信息
-x 显示详细信息
-V 显示版本信息
```

## 4、命令例子

```shell
iostat -d -k 1 10 #查看TPS和吞吐量信息
iostat -d -x -k 1 10 #查看设备使用率（%util）、响应时间（await）
iostat -c 1 10 #查看cpu状态
```
#### 参数 -m使用 M 为单位显；1 5表示，数据显示每隔1秒刷新一次，共显示5次。
```shell
# iostat -m 1 5

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           2.61    0.00    0.10    0.06    0.00   97.24

Device             tps    MB_read/s    MB_wrtn/s    MB_read    MB_wrtn
loop0             0.00         0.00         0.00          1          0
loop1             0.00         0.00         0.00          0          0
loop2             0.18         0.00         0.00         10          0
loop3             0.00         0.00         0.00          0          0
loop4             0.00         0.00         0.00          1          0
loop5             0.00         0.00         0.00          1          0
loop6             0.01         0.00         0.00          0          0
loop7             0.00         0.00         0.00          0          0
sda               1.85         0.02         0.00       1217        178
sdb               0.54         0.00         0.09         18       4911
loop8             0.00         0.00         0.00          0          0
loop9             0.00         0.00         0.00          0          0
loop10            0.00         0.00         0.00          0          0
```

#### cpu属性值说明：
```shell
%user：CPU处在用户模式下的时间百分比。
%nice：CPU处在带NICE值的用户模式下的时间百分比。
%system：CPU处在系统模式下的时间百分比。
%iowait：CPU等待输入输出完成时间的百分比。
%steal：管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比。
%idle：CPU空闲时间百分比。
```

###### 备注：如果%iowait的值过高，表示硬盘存在I/O瓶颈，%idle值高，表示CPU较空闲，如果%idle值高但系统响应慢时，有可能是CPU等待分配内存，此时应加大内存容量。%idle值如果持续低于10，那么系统的CPU处理能力相对较低，表明系统中最需要解决的资源是CPU。


#### disk属性值说明：
```shell
rrqm/s: 每秒进行 merge 的读操作数目。即 rmerge/s
wrqm/s: 每秒进行 merge 的写操作数目。即 wmerge/s
r/s: 每秒完成的读 I/O 设备次数。即 rio/s
w/s: 每秒完成的写 I/O 设备次数。即 wio/s
rsec/s: 每秒读扇区数。即 rsect/s
wsec/s: 每秒写扇区数。即 wsect/s
rkB/s: 每秒读K字节数。是 rsect/s 的一半，因为每扇区大小为512字节。
wkB/s: 每秒写K字节数。是 wsect/s 的一半。
avgrq-sz: 平均每次设备I/O操作的数据大小 (扇区)。
avgqu-sz: 平均I/O队列长度。
await: 平均每次设备I/O操作的等待时间 (毫秒)。
svctm: 平均每次设备I/O操作的服务时间 (毫秒)。
%util: 一秒中有百分之多少的时间用于 I/O 操作，即被io消耗的cpu百分比
```
###### 备注：如果 %util 接近 100%，说明产生的I/O请求太多，I/O系统已经满负荷，该磁盘可能存在瓶颈。如果 svctm 比较接近 await，说明 I/O 几乎没有等待时间；如果 await 远大于 svctm，说明I/O 队列太长，io响应太慢，则需要进行必要优化。如果avgqu-sz比较大，也表示有当量io在等待。





- 如果 %util 接近 100%，说明产生的I/O请求太多，I/O系统已经满负荷，该磁盘可能存在瓶颈。 idle小于70% IO压力就较大了，一般读取速度有较多的wait。
同时可以结合vmstat 查看查看b参数(等待资源的进程数)和wa参数(IO等待所占用的CPU时间的百分比，高过30%时IO压力高)。
        

- 另外 await 的参数也要多和 svctm 来参考。差的过高就一定有 IO 的问题。avgqu-sz 也是个做 IO 调优时需要注意的地方，这个就是直接每次操作的数据的大小，如果次数多，但数据拿的小的话，其实 IO 也会很小。如果数据拿的大，才IO 的数据会高。也可以通过 avgqu-sz × ( r/s or w/s ) = rsec/s or wsec/s。也就是讲，读定速度是这个来决定的。
svctm 一般要小于 await (因为同时等待的请求的等待时间被重复计算了)，svctm 的大小一般和磁盘性能有关，CPU/内存的负荷也会对其有影响，请求过多也会间接导致 svctm 的增加。await 的大小一般取决于服务时间(svctm) 以及 I/O 队列的长度和 I/O 请求的发出模式。如果 svctm 比较接近 await，说明 I/O 几乎没有等待时间；如果 await 远大于 svctm，说明 I/O 队列太长，应用得到的响应时间变慢，如果响应时间超过了用户可以容许的范围，这时可以考虑更换更快的磁盘，调整内核 elevator 算法，优化应用，或者升级 CPU。

