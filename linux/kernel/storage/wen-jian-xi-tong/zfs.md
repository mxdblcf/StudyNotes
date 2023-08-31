# ZFS

#### 命令集合

以下是 `zpool` 命令的 Markdown 文档(by chatgpt)：

## ZFS 池管理命令

### 创建一个新的 ZFS 池

```shell
sudo zpool create <pool_name> <device>
```

`<pool_name>`：要创建的池的名称
`<device>`：用于创建池的设备（硬盘或分区）

### 显示所有可用的 ZFS 池

```shell
zpool list
```

此命令将显示当前系统上所有的 ZFS 池以及与之关联的信息，如名称、大小、使用情况等。

### 显示特定 ZFS 池的详细信息

```shell
zpool status <pool_name>
```

`<pool_name>`：要查看详细信息的 ZFS 池的名称

### 导入一个已经存在的 ZFS 池

```shell
sudo zpool import <pool_name>
```

`<pool_name>`：要导入的 ZFS 池的名称

### 卸载一个已经导入的 ZFS 池

```shell
sudo zpool export <pool_name>
```

`<pool_name>`：要卸载的 ZFS 池的名称

### 添加新的设备到现有的 ZFS 池

```shell
sudo zpool add <pool_name> <device>
```

`<pool_name>`：要添加设备的 ZFS 池的名称
`<device>`：要添加的新设备

### 移除 ZFS 池中的设备

```shell
sudo zpool remove <pool_name> <device>
```

`<pool_name>`：要移除设备的 ZFS 池的名称
`<device>`：要移除的设备

### 检查和修复 ZFS 池中的错误

```shell
sudo zpool scrub <pool_name>
```

`<pool_name>`：要检查和修复错误的 ZFS 池的名称

这只是一些常见的 `zpool` 命令示例，ZFS 还有更多的功能和选项可以用于管理和操作 ZFS 池。你可以使用 `man zpool` 命令在终端中查看完整的 `zpool` 命令文档和选项，以获取更多详细信息和帮助。

希望这个 Markdown 文档对你有所帮助！

