# ctags和tmux插件的使用

### ctags的安装

在Linux的环境下我们在看源代码的时候有的时候想要去了解一些系统自己带的或者自己写的函数的定义，这个时候就需要用ctags这个插件了。

```shell
sudo apt-get install ctags
```

ctags生成相对路径

```shell
ctags -R
```

ctags生成绝对路径

```shell
ctags -R `pwd`
```

查看某个函数定义：

```
ctrl + ]
```

退回上一个函数

```
ctrl + t
```

### tmux的安装

安装命令

```shell
sudo apt install tmux
```

修改tmux 的相应配置文件

```shell
vim .tmux.conf
```

在配置文件中修改为如下内容

```shell
unbind C-b
set -g prefix C-a

bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
```

在终端输入命令进入tmux模式

```
tmux
```

新建一个会话的命令，这三个键一起按可以建立两个会话，这两个会话可以将终端左右分成两部分。

```
ctrl a %
```

![1540736311056](./img\1540736311056.png)

如果按这三个键可以将屏幕分成上下两部分。

```
ctrl a "
```

![1540736443498](.\img\1540736443498.png)

我们可以看到在左边的会话中上下又被分出一个新的会话。

退出某一个会话的操作

```
exit
```

会话之间的切换

```
ctrl a 加上上下左右方向键。
```

