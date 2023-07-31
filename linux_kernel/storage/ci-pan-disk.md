# 磁盘disk

> 关键词： sector（扇区-物理存在的，一般是512byte,是机械磁盘的最小存储单位，ssd固态的话最小单位是page4k） block（逻辑块，文件系统的最小存取单位，一般是4k，也就是文件系统每次拿就是拿8个连续的扇区）

### 初始化

初始化会用到两种方式 **MBR(主引导记录)、GPT(分区表)**

> 假设一个20T磁盘，分5块， （两个命令fdisk2T分区，parted大于2T）

```bash
parted /dev/sda 
   #进入选择m是help,接下来需要创建一个分区表   g ,w 
```

![image.png](https://cdn.nlark.com/yuque/0/2023/png/22337396/1680748305244-bc487dd6-6273-4e42-b8ce-9d0e7e8a7e99.png#averageHue=%232d2928\&clientId=u9b66e2a4-e8cb-4\&from=paste\&height=544\&id=u36a605d8\&originHeight=544\&originWidth=752\&originalType=binary\&ratio=1\&rotation=0\&showTitle=false\&size=57378\&status=done\&style=none\&taskId=u3a3d6cc6-585c-4196-8d48-b142c4971f4\&title=\&width=752)

### NAS 和 SAN 的区别

> NAS(网络附加存储) SAN（存储区域网络）
>
> &#x20;1.NAS主要用于网络间的数据共享(慢) SAN相当于网络上的硬盘(快),通过块级存储访问底层磁盘或RAID(FC、ISCI等块级协议)，应用于数据库存储，虚拟机存储 ，而且成本高&#x20;
>
> 2\.
