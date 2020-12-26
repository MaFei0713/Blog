## Loop回环设备

> 在Linux中，如果想在文件管理系统中再创建另外的文件系统，需要使用回环设备。其支持将以一个普通磁盘文件虚拟成一个块设备（磁盘），对其所有的读写都将被重定向到该普通磁盘文件上。基本操作步骤：

- 创建普通磁盘文件
- 关联回环设备
- 格式化设备文件系统格式
- 挂在该回环设备至挂在点进行写入

下面介绍创建一个Linux回环文件系统的操作步骤：

1. 创建一个空的磁盘文件，使用dd命令：`dd if=/dev/zero of=/var/tmp/c0d0 bs=100M count=1`

2. 将磁盘文件关联到回环设备：`losetup /dev/loop0 /var/tmp/c0d0`;  
	回环设备以`/dev/loop0`,`/dev/loop1`等命名，可使用`losetup /dev/loop0`命令测试回环设备是否为空（可关联），如果返回形如：No such file or directory 即表示该设备为空可以关联。

3. 格式化设备：`mkfs.ext4 /dev/loop0`
4. 创建挂在点：`mkdir /mnt/test_ext4`
5. 挂在设备：`mount /dev/loop0 /mnt/test_ext4`

至此,已将当前文件系统中的/var/tmp/c0d0文件，通过回环设备/dev/loop0挂载至/mnt/text_ext4目录下，并格式化成ext4格式，可在该目录下测试ext4文件系统

使用结束后，需要卸载这个新的文件系统，可使用 `losetup -d`命令，具体操作如下：

1. 卸载挂载：`umount /mnt/test_ext4`
2. 删除关联：`losetup -d /dev/loop0`

以上是对Linux回环设备的简单介绍及使用测试，更多知识，还须要不断研究学习