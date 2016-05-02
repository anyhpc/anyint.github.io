


在 opensuse 中安装 matlab时候，
sudo ./install 后出现报错

Error: Installation cannot proceed. You may either:
1. Set an X11 display, and restart the install process
2. Use the silent install feature by specifying the -mode silent option


解决的方法是 切换到 root用户下，启动图形界面,继续安装就没有问题了

sudo su
 startx
./install

其他的linux版本与此类似

安装完毕后
设置环境变量

sudo vi /etc/profile


在文件末尾添加

export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_71


保存并推出，然后使用下面的命令是设置生效

source /etc/profile