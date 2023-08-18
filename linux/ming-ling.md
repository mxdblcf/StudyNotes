# 命令

### 检测网络带宽 <a href="#step-2-how-to-monitor-your-network-bandwidth" id="step-2-how-to-monitor-your-network-bandwidth"></a>

```bash
 nethogs
 netstat
```

### 磁盘使用情况

```sh
df -h
du
```

### 内存使用情况

```sh
 free -m
```

```bash
// 这样也能
vmstat -S M
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0   6000      3    797    0    0    69    93  228  291  1  1 98  1  0

```
