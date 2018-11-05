#Linux系统及命令行操作熟悉

##【Linux 快捷键】

主键盘快捷键 用左ctrl

- Ctrl + P （对应↑）自下往上搜索history列表里的命令
- Ctrl + N （对应↓）从当前命令开始，自上往下搜索命令
- Ctrl + B （对应←）光标左移
- Ctrl + F （对应→）光标右移
- Ctrl + A  移动到行头
- Ctrl + E  移动到行尾
- Ctrl + H （对应backspace）删除光标前一个字符
- Ctrl + D  删除光标后一个字符（光标覆盖的字符）
- Ctrl + U  删除光标前所有字符
- 在cd路径时 Tab 按一次填充未完成命令或路径，按两次显示子目录或显示可能的命令

##【目录结构 以cd进入】

1. 根目录 ls /
2. /bin  存放最经常使用的命令
3. /boot	开机启动项
4. /dev  外部设备文件
5. /etc  配置文件
6. /home  用户主目录
7. /lib  动态库
8. /lost+found  文件碎片
9. /media 自动挂载外设
10. /mnt手动挂载外设
11. /opt 第三方软件
12. /proc 内存映射
13. /root 超级用户
14. /sbin 管理员用
15. /tmp 临时文件
16. /usr 用户软件

##【用户目录】

1.绝对路径 从根目录开始/home/xst/aa

2.相对路径 bb（相对于当前工作目录）

- . ->当前目录
- .. ->当前的上一级目录	
- -	->临近两个目录切换 cd –

3.xst@xst-VirtualBox:~$

- xst：当前登录用户
- @：在
- xst-VirtualBox：主机名
- ~：宿主目录
- $：普通用户（#为超级用户，即root用户，sudo su切换，exit退出）

##【文件和目录操作】

1.查看文件与目录
 
- cd /home 进入 '/ home' 目录' 
- cd .. 返回上一级目录 
- cd ../.. 返回上两级目录 
- cd 进入个人的主目录 
- cd ~user1 进入个人的主目录 
- cd - 返回上次所在的目录 
- pwd 显示工作路径 
- ls 查看目录中的文件 
- ls -F 查看目录中的文件 
- ls -l 显示文件和目录的详细资料 
- ls -a 显示隐藏文件 
- ls *[0-9]* 显示包含数字的文件名和目录名 
- tree 显示文件和目录由根目录开始的树形结构(1) （要手动下载）
- lstree 显示文件和目录由根目录开始的树形结构(2) 
- cat 在终端上查看文件内容（适合小的文件）
- more 显示更多，空格翻页，Q键退出

2.创建文件与目录

- touch file1 创建一个空文件 
- mkdir dir1 创建一个叫做 'dir1' 的目录' 
- mkdir dir1 dir2 同时创建两个目录 
- mkdir -p /tmp/dir1/dir2 创建一个目录树 

3.删除

- rm -f file1 删除一个叫做 'file1' 的文件' 
- rmdir dir1 删除一个叫做 'dir1' 的空目录' 
- rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容 （-r为递归）
- rm -rf dir1 dir2 同时删除两个目录及它们的内容 
- rm -ri dir1 删除前先询问 （-i为询问）
 
4.拷贝

- cp file1 file2 复制一个文件 ，file2 若不存在，则创建，若存在，则覆盖
- cp dir1 new dir -r. 复制一个目录下的所有文件到另一个目录newdir将被创建
- cp dir1 dir2 -r. 复制一整个个目录到已存在的目录
- cp dir1* dir2 复制目录下的文件到已存在的目录，

5.移动

- mv file1 file2/dir1 重命名/移动 一个文件

6.创建快捷方式

- ln -s dir+file1/dir1 lnk1 创建一个指向文件或目录的软链接 （目录范围可用）
- ln file1 lnk1 创建一个指向文件的物理链接（类似备份）

7.which 命令 查看当前命令从何被调用

8.查看和修改文件权限（目录必须有执行权）

- whoami 查看当前用户

权限（mode）：

- r：read
- w：write
- x：执行
- ：无

文字法：

- chmod  who+/-/=mode file1 给file1的各所有者增加或删减或覆盖权限，不写who默认为所有人
如：
![](https://i.imgur.com/pTIDBYQ.png)

- 第一串字符每三位为不同所有者的权限：文件所有人u/文件所属组g/其他人o
- 还有所有人a

数字法：

- r：4
- w：2
- x：1
- -：0

chmod  777 file1 给file1的所有人加满权限

- 数字代表该位置所有者的权限和

chmod -001 file1 给其他人删除执行权限

9.修改文件所有者（要加sudo）

- chown user1 file1 改变一个文件的所有者 （需要先sudo 借用管理员权限）
- chown user1:group1 file1 改变一个文件的所有者和所属组 
- chgrp group1 file1 改变文件的群组

10.文件的查找和检索

- find dir1 -name “file1” 查找指定文件名的文件 （“”不加会报错） 文件名记不全时，*通配多个字符，？通配一个字符
- find dir1 -size +/- 10k 查找大于或小于指定大小的文件
- find dir1 -size +10k -size -1M 查找范围大小的文件
- find dir1 -type d/f/b/c/s/p 查找指定类型文件 （分别对应目录/文件/块设备/字符设备/socket文件/管道）
- grep -r “string1” dir1 查找含有指定字符串的文件

##【软件的安装与卸载】
1.在线安装

- sudo apt-get install 软件名  安装软件
- sudo apt-get remove 软件名 移除软件
- sudo apt-get update 更新软件列表（存放软件名与下载地址）
- sudo apt-get clean 清楚所有安装包（清理/var/cache/apt/archives下的.deb文件）

2.deb包安装

- Sudo dpkg -i xxx.deb 安装（install）
- Sudo dpkg -r xxx 删除（remove）
	
3.源码安装

会提供readme文件，按它来

##【挂载U盘】

全屏虚拟机自动挂载或设备-USB手动勾选（要插2.0的口），自动挂载在/media下

umount /dir1/用户名/U盘名  删除U盘 dir为/media或/mnt

sudo fdisk -l  查看U盘设备名字（不是你给U盘取的名字）如/dev/sdb1

sudo mount 设备名 /mnt  将U盘挂载到/mnt目录上

##【压缩包管理】
1.简易版 .gz .bz2

- gzip file 压缩文件
- bzip2 file 
- bzip2 -k file 压缩并保留源文件
- gunzip/bunzip2 file 还原文件
	
2.实用版

2.1 .tar

- c-压缩
- x-解压缩
- v-显示提示信息
- f-指定文件名
- z-使用gzip压缩
- j-使用bzip2压缩
- tar zcvf xxx.tar.gz file1/dir1压缩文件或目录，命名为xxx.tar.gz
- tar zxvf xxx.tar.gz 解压缩至当前目录
- tar zxvf xxx.tar.gz -C dir1 解压缩至指定目录
		
2.2 .rar（需手动安装）

- a-压缩
- x-解压缩
- rar a xxx file1/dir1 压缩
- rar x xxx dir1解压缩至指定目录
		
3.3 .zip

- zip xxx file1/dir1 -r 压缩（目录要-r）
- unzip xxx -d dir1 解压缩至指定目录
- 压缩：命令+参数+压缩包的名字+要压缩的文件/目录
- 解压缩：命令+压缩包名字+参数（rar无）+解压目录

##【进程管理】
1. who 查看当前在线用户情况
2. alt +ctrl+F1~F7 切换设备终端（各终端间互不影响）
3. ps a 查看整个系统内部运行的进程
4. ps au 查看详细 PID：进程编号
5. ps aux 查看没有终端的进程 终端：与用户交互
6. | 管道 命令1 |命令2 1的输出作为2的输入，1的输出不显示
7. Ps aux | grep bash 查找系统下所有bash进程（找到>2个才算找到）
8. kill -l 查看进程编号
9. kill -SIGKILL/9 pid 杀死编号为xxx的进程
10. env 查看当前进程的环境变量 PATH=value1:value2:…
11. top 查看任务管理器

##【网路管理】
1. ifconfig  查看本机网路信息
2. ping 测试主机间能否通信
3. nslookup 查看域名对应的ip

##【用户管理】
1. sudo adduser 用户名  添加用户（不能有大写字母）
2. sudo useradd -s shell类型 -g 所属组 -d 用户目录 -m 目录名  添加用户
3. sudo groupadd 目录名  创建用户目录
4. su 用户名  切换用户
5. su/su -/sudo su 切换到root用户
6. sudo passwd 用户名   修改密码
7. exit 退出当前用户
8. sudo deluser 用户名  删除用户
9. sudo userdel -r 删除用户与其宿主目录

##【ftp服务器搭建（安装vsftpd）】

负责文件的上传与下载

1. 服务器端

修改配置文件 

- cd /etc
- sudo gedit vsftpd.conf  调整或放开以下参数（:wq保存）

![](https://i.imgur.com/tBboNJD.png)

重启服务 sudo service vsftpd restart （使修改生效）

2. 客户端

实名用户登录 

- ftp 服务器端的IP
- 服务器名字
- 服务器密码
- put file1 从登录目录上传文件	
- get file1 从ftp所处目录下载文件
- 要操作目录必须打包

匿名用户登录（更安全,不允许随意切换目录）

- ftp 服务器端的IP
- 用户名：anonymous
- 密码：回车跳过
			
创建匿名用户使用的目录：

- 在服务器根目录中mkdir dir1，并打开其他人的write权限
- 在/etc/vsftpd.conf 中添加 anon_root=服务器根目录/创建的目录

退出：quit或bye

lftp客户端访问ftp服务器（要安装lftp）

- lftp 服务器ip
- login
- lcd dir1 修改本地目录
- mput file1 file2 上传多个文件
- mget file1 file2 下载多个文件
- mirror dir1 上传目录
- mirror -R dir1 下载目录

##【nfs服务器搭建（安装nfs-kernel-server）】
1.服务器端

- 创建共享目录 mkdir dir1
- 修改配置文件 /etc/exports里添加 共享目录 *(权限,sync)
- 重启服务sudo sevice nfs-kernel-server restart

2.客户端

mount 服务器IP:共享目录 /mnt  挂载共享目录.，登录 

##【ssh服务器】
1.远程访问

- ssh 服务器名字@服务器IP
- Are you sure…..? yes
- logout 退出登录

2.scp命令（安装openssh-server）

- scp == super copy
- scp -r 目标用户名@目标IP:/目标文件的绝对路径 /保存到本机的路径

##【其他命令】
1. man man 查看man文档（1.2.3.5章常用）
2. alias 命令  查看命令是否被封装过
3. echo “xxxx” 输出指定字符串xxxx
4. echo $xxxx 输出key xxxx中的value
5. sudo poweroff 关机
6. sudoreboot 重启
7. shut down 

##【vim编辑器的使用（安装vim）】
1.命令模式（按两下esc从其他模式回到命令模式）

vi xxx.txt  打开文本文件

: 切换至末行模式

1.1光标移动：

- h左移			
- gg 文件头部（行）
- j下
- G 文件尾部（行）
- k上				
- xxG 移动到第xx行
- l右
- 0 行首
- $ 行尾
 
1.2删除（其实是剪切）： 

- X/x 删除光标前/后的字符
- dw 删除单词光标后的部分
- d0/d$（或D） 删除当前行光标前/后的内容
- dd 删除光标所在行
- ndd 删除光标所在行与其下面行，一共n行
- u 撤销
- ctrl+R 反撤销

1.3复制粘贴

- p 从光标下一行粘贴
- P粘贴到光标行
- yy 复制（nyy类似ndd）
- v 进入可视模式（移动光标复制y/剪切d部分内容，但粘贴时不带换行）

1.4查找

- / xxx（或? xxx） 查找字符xxx，按n/N向下/上切换
- r+x 用x替换光标所在字符（单个）

1.5缩进

- >>/<< 向右/左

1.6查看man文档：

- 光标移动到对应单词后，按K/nK  查找/去第n章查找

2.编辑模式（在命令模式下操作）

- a/A  从光标后/行尾开始输入
- i/I  从光标前/行首开始输入
- o/O  从光标下/上创建新行并输入
- s/S  删除光标后/光标所在行的内容并输入

3.末行模式（以:进入,回车执行）

- :xxx 跳到xxx行
- :s/xxx/mmm 替换光标所在行第一个字符xxx为mmm
- :s/xxx/mmm/g 替换光标所在行所有字符xxx为mmm
- :%s/xxx/mmm 替换光标所在行第一个字符xxx为mmm
- :n,ms/xxx/mmm 替换第n至第m行第一个字符xxx为mmm
- :!命令  执行命令
- :w/:q/:wq/:q!  保存/退出/保存并退出/退出不保存 x==wq
- ZZ 命令模式下保存退出

4.分屏

末行模式下

- :sp/:vsp 当前文件水平/垂直分屏
- :sp file1 水平分屏打开另一个文件
- Ctrl+ww 屏间切换

5.打造IDE

- /etc/vim/vimrc 系统级修改
- ~/.vim.vimrc	用户级修改

##【gcc编译器】
1.分步

- gcc -E xxx.c -o xxx.i 预处理
- gcc -S xxx.i -o xxx.s 编译
- gcc -c sum.s -o xxx.o 生成二进制文件
- gcc xxx.o -o name 生成可执行文件

2.一步

- gcc xxx.c -o name  直接生成二进制文件
- gcc xxx.c -I dir1 -o name 指定头文件目录并执行

3.参数

- -D宏名称  编译时指定宏
- -O0/1/2/3  优化，程度由小到大
- -Wall 提示更多警告信息
- -g 添加调试信息
 
##【静态库的制作】
1.命名规则

- lib+name.a

2.制作步骤

1. 生成.o
2. 打包 ar rcs libxxx.a *.o
 
3.发布与使用

调用了哪个，就打包相应的.o，带上头文件

gcc main.c libxxx.a -o mmm -I dir1

4.优缺点

1. 发布时不需要提供库/程序体积大
2. 加载速度快/库改变需重编译

##【动态库的制作】
1.命名规则

- lib+name.so

2.制作步骤

1. 生成与位置无关的.o  gcc -FPIC -c *.c
2. 打包 gcc -shared -o libxxx.so *.o

3.发布与使用

4.若无法被加载

- ldd appname 查看程序执行时调用的动态库
- export LD_LIBRARY_PATH=动态库的路径  临时解决
- 1.找到动态链接库的配置文件/etc/ld.so.conf
- 2.动态库的路径写入配置文件
- 3.更新 sudo ldconfig

5.优缺点

1. 体积小/需提供给客户
2. 更新不需重新编译（接口变了还是要更新）/加载慢












