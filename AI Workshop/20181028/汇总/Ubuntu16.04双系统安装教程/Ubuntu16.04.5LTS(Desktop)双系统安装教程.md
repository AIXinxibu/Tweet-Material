
#Ubuntu 16.04.5 LTS 双系统安装教程

##【安装】

安装平台：acer VN7 591G笔记本（每个人都不一样），带win10 1803版，UEFI启动，GPT分区
Linux系统包：Ubuntu桌面版 16.04.5 LTS（64位），技术支持至2021年4月

##【下载镜像】

1.下载地址：https://www.ubuntu.com/download/alternative-downloads

2.滚动至BitTorrent栏，点击Ubuntu 16.04.5 Desktop (64-bit)下载种子文件。亲测校园网环境下使用迅雷下载速度17MB/s，两三分钟即可下载完成

![](https://i.imgur.com/Q1Wec9Y.png)

##【写镜像】

1.下载UltraISO（软碟通）

- 下载地址：https://pan.baidu.com/s/14DyGbH3-w-TozoyKAduU8w
- 备用地址：https://www.lanzous.com/i1ypckh

2.打开软件，文件-打开-选择刚刚下载的ISO文件

![](https://i.imgur.com/mmlnuTP.png)

3.插入U盘，启动—写入硬盘映像…

![](https://i.imgur.com/Pe8tXhM.png)

4.确认U盘和ISO文件位置无误，依次点击“格式化”和“写入”。写入完成后进度条满，消息窗口提示“刻录成功！”

![](https://i.imgur.com/Xz55TBp.png)

##【磁盘准备】

1.桌面——右击“我的电脑”——右键菜单下点击“管理”，进入计算机管理页面。左边点击磁盘管理，出现类似下图的界面。（或快捷键Win+X，选择磁盘管理）

![](https://i.imgur.com/NpRO4Nx.png)

2.选择一个分区点击“压缩卷”，出现以下界面。压缩空间处建议至少输入40960MB，若可用压缩空间不足，选择其他分区或者挪动文件满足安装需求。（此计算机直接删除了某100GB分区用于双系统，此图空间不足）

![](https://i.imgur.com/tTxsoMe.png)

3.点击压缩后，会出现40g以上的未分配空间，无须格式化。至此，你已经有空间去放置你的Ubuntu系统了（此处盗图，可见该同学压缩了50G空间）

![](https://i.imgur.com/6sTzBcn.png)

##【BIOS设置】

1.关闭快速启动（避免安装出现其他问题，建议关闭）。右击桌面右下角的电源图标，选“电源选项”（或快捷键Win+X选电源选项，右侧“相关设置-其他电源设置”），在新窗口中点击“选择电源按钮选项”，在跳转窗口中点击“更改当前不可用的设置”，去掉“快速启动”的对勾，保存更改

![](https://i.imgur.com/y7UFO1V.png)

![](https://i.imgur.com/T4vweHf.png)

2.设置Secure Boot。插入U盘，重启电脑按F2进BIOS（Acer笔记本为F2，其他电脑可测试F2，F12，Del键，F1等等）。方向键控制光标，向右转到boot页面，Secure Boot设置为Disabled。向下移动光标至USB HDD（写过镜像的U盘），按F6使其成为第一启动项。然后按F10保存退出（或者按方向键右转到exit页面选择Exit Saving Changes）

![](https://i.imgur.com/5rtjgry.png)

![](https://i.imgur.com/ZfTPWyy.png)

3.补充：如果Acer电脑发现不能将Secure Boot 设置成Disable，就得去Security里面设置一下 Supervisor password就行了

![](https://i.imgur.com/sxA2WOR.jpg)

##【安装Ubuntu】

1.退出BIOS后，自动重启。刚刚设置过U盘为第一启动项，此次将启动U盘的Ubuntu安装程序而不启动windows。开启电脑，即可进入U盘安装界面了，这个时候我们选择Install Ubuntu即可

![](https://i.imgur.com/aPOMU0z.png)

2.然后就是选择语言了，选择自己合适的语言就行了，我选择了中文，点击继续

![](https://i.imgur.com/g5GoPab.png)

3.接下来就是连接WiFi，安装图形界面了，大家可以根据自己的网络情况是否连接WiFi。这个影响不大。为了缩短安装时间，我选择的不联网，继续，不安装更新，不安装第三方软件，继续

![](https://i.imgur.com/R4odJu9.png)

![](https://i.imgur.com/UumJkMo.jpg)

4.好了，到了最关键的一步了，这个时候系统会提示你是否与windows 10 共存，我们不要点击那个，我们选择“其他选项”，这样自己方便管理一些。 

注意：如果系统没提示你之前安装过windows 那么你的启动方式就错误了，你得回到BIOS页面下更改启动方式再次启动

![](https://i.imgur.com/kVbVoIf.png)

5.下面需来对Ubuntu进行分区，在分区之前先介绍一下Linux的文件系统。
- 
- swap：用作虚拟内存，这个一般和自己的物理内存一般大
- /：主要用来存放Linux系统文件
- /boot：存放linux内核，用来引导系统的，如果是Legacy启动就要设置引导，UEFI就不用设置这个（UEFI要设置EFI文件）
- /usr：存放用户程序，一般在/usr/bin中存放发行版提供的程序，用户自行安装的程序默认安装到/usr/local/bin中
- /home：存放用户文件

我们在看磁盘信息的时候可以发现自己当初没有分配的那个空闲磁盘（如我的100GB在图中显示107375MB空闲），选中那个空闲磁盘，然后点击左下角的“+”号，开始分配。后续每次分配均需要选中空闲磁盘，再点击“+”

![](https://i.imgur.com/eEYfm6h.jpg)


6.分配swap。我们选择主分区，空间起始位置，大小和自己物理内存一样（我的是12G我就分配12288M），用于交换空间

![](https://i.imgur.com/glBg7tm.jpg)

7.设置引导（下面两个根据自己启动方式选择其一）

选择空闲磁盘，点击“+”。

- 设置EFI引导，我们选择逻辑分区，空间起始位置，用于EFI系统分区，大小设置500M即可，由于空间较大，我设置了800MB。（Legacy启动的话就没有这个所以Legacy启动可以跳过这步）
- 设置Boot引导，选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/boot，大小设置200M。（UEFI就不用设置，跳过此步）

![](https://i.imgur.com/3xTGiWA.png)

8.设置/分区

设置/，我们选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/，大小的话推荐8-16G，可以根据自身情况设置，我这里设置的是16G。

![](https://i.imgur.com/jIuUqtn.png)

9.设置home分区

设置/home，我们选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/home，大小的话可以根据自身情况，如果偏爱娱乐方面的话可以设置大一点，这里我设置的是36G

![](https://i.imgur.com/iMlkVTs.png)

10.设置usr分区

设置/usr，我们选择逻辑分区，空间起始位置，用于Ext4日志文件，挂载点：/usr，大小的话剩余的空间就都给它了

![](https://i.imgur.com/6uCchrr.png)

11.设置完所有以后，我们要将下面的安装启动器设备换成我们刚刚设置引导的那个盘

![](https://i.imgur.com/cOaPw5E.jpg)

12.接着，一系列默认……

![](https://i.imgur.com/qpA8lJL.jpg)

![](https://i.imgur.com/x4UWF01.jpg)

![](https://i.imgur.com/PrFVWUY.png)

13.设置用户及密码

![](https://i.imgur.com/SjIqbOT.jpg)

14.等待安装完成

![](https://i.imgur.com/NgDduqd.jpg)

![](https://i.imgur.com/edvJrZU.jpg)

15.在BIOS里面添加EFI文件（Legacy启动忽略此步）

由于我们虽然设置了EFI启动文件但是没有在BIOS里面添加，所以安装完成以后我们还要进BIOS ，还是老步骤，开机一直按F2进入BIOS，Acer电脑的话进入BIOS就要输入我们之前设置的密码了。我们选择Security 然后Select an UEFI file as trusted for executing ，弹出窗口，进入Ubuntu/BOOT/grubx64.efi。接着添加备用名，随手填Ubuntu。F10保存重启后，可以看到BIOS里已有Ubuntu项，按F6设置其为第一或第二启动项，保存重启

![](https://i.imgur.com/Md8l39C.png)

![](https://i.imgur.com/IzVPEL9.png)

![](https://i.imgur.com/H97Y0Pq.png)

16.重启后，若成功引导，则会出现下面界面（我的笔记本据说是因为主板默认windows系统启动，只能按F12才能进入系统选择界面）。选择第一项Ubuntu

![](https://i.imgur.com/Cyo8x15.png)

17.用之前设置的账户密码登录后，出现以下界面。至此，Ubuntu安装完成。

![](https://i.imgur.com/4yqTZ35.jpg)
