
---
title: solve [FAILED] Failed to start Load Kernel Modules
---
 ## 安装opensuse13.2 系统更新后，开机引导内核时候每次都出现

``` bash
$ [FAILED] Failed to start Load Kernel Modules
See "systemctl status systemd-modules-load.service" for details.
......
```
虽然不影响使用，但是也看着不爽，今天终于没有拖延了，解决了这个问题，记录如下
第一步:查

使用如上关键词依次在 baidu bing google 上查询了一遍
这个问题在baidu上只能找到贴吧上的一个帖子但是没有给出解决方案，大部分都是讲关于虚拟机的问题，
在bing上找到了一个有用的线索，但是还是没有看明白，但google 上给出了大量的中英文信息。
主要参考了 这个帖子
https://bbs.archlinux.org/viewtopic.php?id=187529
里面两个人对话 讲到分别在 /etc/modules-load.d/ 和 /usr/lib/modules-load.d 文件夹中查看有没有文件
并解决了问题，我就甩开膀子开干了
第二步：试

我打开上述两个文件夹，第一个文件夹也是空的，但是在第二个文件夹里找到了两个文件。
将这两个文件 复制到主文件夹中新建的临时文件目录，以免删除错了来恢复
这两个文件分别是 bbswitch.conf sg.conf
里面文件内容如下 ：
``` bash
bbswitch.conf

bbswitch

sg.conf
```
	
``` bash
# load sg module at boot time
sg
```
然后 我就用sudo rm s* b* 删除了这两个文件了
接下来 参考了另一篇博文
chen.junchang.blog.163.com/blog/static/6344519201503135322287/
使用了 ``` sudo mkinitrd ``` 重新生成启动映像
生成过程中产生了一堆堆引导modules的错误，不知道是不是没有插入软件源U盘的原因。
然后重启
第三步：查

重启后心惊胆跳地等待，没有报错，谢天谢地，
我等学渣基础不牢固，做事情总是自己对自己都不放心的

最后，记录此文以给自己和读者参考

