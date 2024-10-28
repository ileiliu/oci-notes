---
title: Working with Block Volumes
date: 2023-08-25 19:15:39

---

虽然 OCI Linux 系统默认驱动盘容量为46.6GB，但是可以在OCI中在线扩展引导卷的大小，而不会出现任何停机时间。


<!--more-->

# 1.创建数据磁盘
参考[Creating a Block Volume](https://docs.oracle.com/en-us/iaas/Content/Block/Tasks/creatingavolume.htm)创建数据磁盘。

# 2.附加数据磁盘
附加类型有两种：iSCSI 和 Paravirtualized Attached。两种附加方式的差异，可以参考[Volume Attachment Types](https://docs.oracle.com/en-us/iaas/Content/Block/Concepts/overview.htm#attachtype)。两种附加方式的磁盘性能差异，可以参考 [VM Shapes for iSCSI-attached Volumes](https://docs.oracle.com/en-us/iaas/Content/Block/Concepts/blockvolumeperformance.htm#Block_Volume_Performance) 和 [VM Shapes for Paravirtualized Attached Volumes](https://docs.oracle.com/en-us/iaas/Content/Block/Concepts/blockvolumeperformance.htm#Block_Volume_Performance)


## 3.通过 iSCSI 附加磁盘

### Use Oracle Cloud Agent to automatically connect to iSCSI-attached volumes 

#### enable the Block Volume Management plugin on the instanc
To automatically connect to the volume, the Block Volume Management plugin must be enabled on the instance. 
When enabling the Block Volume Management plugin, ensure that the instance is running version 1.23.0 or newer of the Oracle Cloud Agent software.

https://www.cnblogs.com/liujiaxin2018/p/13866515.html





# 挂载大于 2 TB 的 磁盘（fdisk不适合大于2TB的volume）
## 分区
https://erdong.site/tools/parted-create-gpt-partition.html


## 挂载
标签
parted -s -a optimal -- /dev/nvme0n1 mklabel gpt

分区
parted -s -a optimal -- /dev/nvme0n1 mkpart primary 0% 100%

格式化
mkfs.xfs /dev/nvme0n1p1

挂载
mount /dev/nvme0n1p1 /data



# 查看磁盘UUID
blkid


# 参考文档：

https://erdong.site/tools/parted-create-gpt-partition.html


# fdisk
https://www.cnblogs.com/liujiaxin2018/p/13866515.html
https://blog.csdn.net/richerg85/article/details/17917129

https://www.jinbuguo.com/systemd/systemd.automount.html#

https://www.jinbuguo.com/systemd/systemd.mount.html

https://wiki.archlinuxcn.org/wiki/Fstab?rdfrom=https%3A%2F%2Fwiki.archlinux.org%2Findex.php%3Ftitle%3DFstab_%28%25E7%25AE%2580%25E4%25BD%2593%25E4%25B8%25AD%25E6%2596%2587%29%26redirect%3Dno