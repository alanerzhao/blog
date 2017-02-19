title: easybcd实现WIN 7+Ubuntu双系统
tags:
  - ubuntu
  - windows7
id: 25
categories:
  - linux
date: 2012-05-06 06:59:48
---

        现在想从事前端了，虽然一直在搞XHTML、CSS相关，并不涉及到Ubuntu但是，我喜欢一个编辑器，那就是Vim，虽然我在WIN下可以使用gVim，但是效果肯定没有Linux下的要好，另一方面，我以前就一直很喜欢Linux，现在已经淡忘的差不多了，所以想把Linux拾起来，以下是我结合网络资料，安装方法当然有好多，有用grub4dos的，也有用LiveCD的也有用本文将要叙述的，大千世界无所不用，我用的是easybcd这个可能是比较菜鸟级别的，所以我也选择了它。总结的安装心得，可以存在错误，还希望指正。

<!--more-->

相关软件及系统：

1.  ubuntu-11.10-desktop-i386下载地址：[http://www.ubuntu.com/download/ubuntu/download](http://www.ubuntu.com/download/ubuntu/download)
2.  easyBCD 下载地址：[http://www.softpedia.com/get/System/OS-Enhancements/EasyBCD.shtml](http://www.softpedia.com/get/System/OS-Enhancements/EasyBCD.shtml)
3.  WIN 7 下载地址：(自行google，推荐远景)
4.  UltraISO|软碟通 下载地址：(自行google)
5.  WIN 7系统已经安装好，这个不想在多说，相信大家都会安装。
6.  安装easybcd这个和平常的软件一样，一路next下去便可以。
7.  当前系统已经有linux的分区了，也就是有一个空白的分区，这里可以google如何分区比较合理，这里不在多说。然后就是用软碟通，解压ubuntu-11.10-desktop-i386.iso文件 然后把casper文件下的initrd.lz和vmlinuz文件拷到C盘根目录待用。
8.  配置easybcd,打开安装好的easybcd
9.  点击Install之后旁边的配置就可以打开了，然后就在配置文件里添加如下内容
> title Install Ubuntu> 
> root (hd0,0)> 
> kernel (hd0,0)/vmlinuz boot=casper iso-scan/filename=/ubuntu-11.10-desktop-i386.iso ro quiet splash locale=zh_CN.UTF-8> 
> initrd (hd0,0)/initrd.lz
注意这里ubuntu-11.10-desktop-i386 就是我们下载的系统文件 如果是其他版本 ，或名字不一样要改过来。
这里要注意了，（hd0,0）表示第几块硬盘的第几个分区，如果是win7可能有个100M的隐藏分区，要改成（hd0,1）这样才能找到C盘

> title Install Ubuntu> 
> root (hd0,1)> 
> kernel (hd0,1)/vmlinuz boot=casper iso-scan/filename=/ubuntu-11.10-desktop-i386.iso ro quiet splash locale=zh_CN.UTF-8> 
> initrd (hd0,1)/initrd.lz
注意这里ubuntu-11.10-desktop-i386 就是我们下载的系统文件 如果是其他版本 ，或名字不一样要改过来。
注意:（hd0,0）表示第几块硬盘的第几个分区，如果是win7可能有个100M的隐藏分区，要改成（hd0,1）这样才能找到C盘
重启 你就会看到有2个 启动菜单给你选择 我们选择第2个 NeoGrub 这个
然后等待一段时间 就会见到ubuntu的安装界面，然后就是ctrl+shift+t打开终端，输入代码:sudo umount -l /isodevice这一命令取消掉对光盘所在 驱动 器的挂载，否则分区界面找不到分区。
然 后就开始安装了，有3个选项 ， 选择最后一个 ，就是安装到我们指定的分区，关于ubutun分区自己去百度查查把 一大堆的帖子。我这里是分了三个区，因为我的内存是2G的所以分了2048的swap交换分区。然后给了/boot的一个150M的分区，然后全都给了 /根分区。然后一路安装下去。
**两种方案：**
第一种：*注意下面的引导安装位置，我选择的是安装到了/分区的位置，而不是默认的 位置*这样的话启动之后不会出现ubuntu的grub引导，而是windows引导，因为我在上面没有替换windows的引导。这也是我想要那种双系 统。然后就是进入windows7,删除C盘下的系统和initrd.lz和vmlinuz。然后打开 easybcd删除neogrub，再添加一个ubuntu的引导。这样重启以后就会出现两个启动项了。
第二种：引导安装位置默认不要改变，就会替换windows的引导，一路安装下去，这样重启之后就会出现grub代替了windows的引导最下面会出来windows7的引导，而且可以进入的。这样也实现了双系统。
然后去windows下我们的c盘 删除vmlinuz，initrd.lz和系统的iso文件，打开easybcd删除neogrub
**后记配置：**
一切都搞定了 就是win7现在不是默认的 而是最后一个 ， 打开终端 输入 sudo gedit /boot/grub/grub.cfg 然后找到有关 windows的 剪切粘贴 到第一启动项的上面 重启就行了。
**遇到问题及折腾总结：**
恢复 windows mbr启动
下载mbrfix.exe放到c盘根目录
进入命令提示符也就是 cmd，输入cd  / 进入根目录
输入mbrfix /drive 0 /yes (注意空格)回车
在windows7下可能提示没有权限，那你可以右击mbrfix给他一个管理员权限便 可以。
在这里我遇到的问题就是，系统进不去了，提未 no stytemfile 我的解决办法，做了一个u盘的系统，进去之后，在安装界面按shift+F10, 然后输入cmd在输入bootrec /fixmbr
这样也就恢复了windows的启动了，不用等的长时间重装系统了，这里直为解决问题哦。
**Grub4Dos****实现WIN 7+Ubuntu双系统**
这个方法和上面的方面类似，也可以说一下面大体说一步骤

*   下载最新版本的 Grub4DOS [http://sourceforge.net/projects/grub4dos/](http://sourceforge.net/projects/grub4dos/)，
*   下载并解压缩后，将目录中的 grldr , grldr.mbr， grub.exe 三个文件复制到 C 盘根目录下。
注意：如果你存在隐藏分区，请把隐藏分区加上驱动盘符号例如A，然后把这些文件都放入隐藏分区，而不是C盘

*   在下载好的 ubuntu-11.10-desktop-i386.iso 文件中， casper 文件夹目录下，找到 vmlinuz、initrd.lz 解压，并复制到 C 盘根目录下。
*   C 盘根目录下建立menu.lst 文件，内容为：

> title Install Ubuntu> 
> root (hd0,0)> 
> kernel (hd0,0)/vmlinuz boot=casper iso-scan/filename=/ ubuntu-11.10-desktop-i386.iso ro quiet splash locale=zh_CN.UTF-8> 
> initrd (hd0,0)/initrd.lz
注意:（hd0,0）表示第几块硬盘的第几个分区，如果是win7可能有个100M的隐藏分区，要改成（hd0,1）这样才能找到C盘 ，这个文件如果你有隐藏分区也要放到隐藏分区里面。
ubuntu-11.10-desktop-i386.iso就是你的要安装的镜像名
在C 盘根目录新建一个文件命名为boot.ini 。 内容如下：
> [boot loader]> 
> [operating systems]> 
> c:\grldr.mbr="Ubuntu"
注意：同上如果存在隐藏分区，同样放到隐藏分区里。</p>

1.  将下载的ubuntu-11.10-desktop-i386.iso文件复制到C盘根目录。
2.  重启机器。在启动项选择Ubuntu. 进入Ubuntu桌面。打开终端，输入代码:sudo umount -l /isodevice这一命令取消掉对光盘所在 驱动 器的挂载，否则分区界面找不到分区。
下面的安装步骤同上面的一样了。所以不在叙述。