# Linux 常用命令

Linux里面一切皆文件

## 基本快捷键

|     按鍵      |          作用          |
| :-----------: | :--------------------: |
|    CtrL+d     |        退出终端        |
|    Ctrl+s     | 暂停程序运行，再按恢复 |
|     Home      |     光标移动至行头     |
|      End      |      光标移至行尾      |
|    Ctrl+k     | 删除光标当前位置至行尾 |
| Alt+Backspace |     删除前一个单词     |
|      Tab      |        补全命令        |

## 通配符

类似正则表达式

|      字符       |            含义            |
| :--: | :--: |
|        *        |      匹配0或多个字符       |
|        ?        |        匹配任一字符        |
|     [list]      | 匹配list中任意一个单一字符 |
|     [^list]     |  匹配除list中字符外的字符  |
|     [c1-c2]     |   匹配c1-c2中任一个字符    |
|    {c1..c2}     |    匹配c1-c2中全部字符     |
| {str1,str2,...} |    匹配str中一字符串    |

## 基本命令

| 命令  |           作用           |
| :---: | :----------------------: |
|  man  |         查看手册         |
|  pwd  |       获取当前所在的绝对路径       |
|  cat  | 读取指定文件并打印到终端 |

## 基础操作

### 用户及用户组

1. 用户操作

   ```linux
   # 添加用户：
   sudo adduser <user>
   # 切换用户
   su <user>
   # 设置密码
   sudo passwd <user>
   # 退出当前用户：ctrl+D
   # 删除用户：
   sudo deluser <user> --remove-home
   ```

2. 用户组操作

   ```
   # 查看所属用户组
   group <user>
   # 将其他用户添加到sudo用户组
   sudo usermod -G sudo <user>
   ```

### 目录

1. `.`表示当前目录，`..`表示上一级目录，`-`表示上一次所在的目录，`~`表示当前用户的`home`目录。绝对路径，简单地说就是以根" / "目录为起点的完整路径，表现形式如：`/usr/local/bin`；相对路径，也就是相对于你当前的目录的路径，相对路径是以当前目录 . 为起点，以你所要到的目录为终点，表现形式如：`usr/local/bin`。如果是当前目录的上一级目录，则需要使用`..`。

2. 多数Linux系统采用*FHS(Filwsystem Hierarchy Standard)* 文件系统层次结构标准，其定义了两层规范：

   - `/`下面的各个目录应该要放什么文件数据，例如` /etc` 应该放置设置文件，`/bin` 与`/sbin` 则应该放置可执行文件等等。
   - 针对 `/usr` 及 `/var` 这两个目录的子目录来定义。例如 `/var/log` 放置系统日志文件，`/usr/share` 放置共享数据等等。

3. 创建多级目录
   ```
   mkdir -p <father>/<son>/<grandson>
   ```

### 文件操作

#### 查看

1. 查看文件权限：一个目录同时具有读权限和执行权限才可以打开并查看内部文件，而一个目录要有写权限才允许在其中创建其它文件。

   ```
   # 查看文件信息
   ll <file>
   # 以更详细信息查看所有文件
   ls -l
   # 更直观查看文件大小
   ls -lh
   # 显示包括隐藏文件（以.开头的文件）
   ls -A
   # 查看某一目录的完整属性
   ls -dl <dr>
   # 显示所有文件大小
   # s为显示文件大小，S为按文件大小排序
   ls -AsSh
   ```

2. `cat`为正序显示,`tac`为倒序显示.
#### 修改文件权限

g/o/u分别表示group/others/user，+/-分别表示增加/减去相应的权限rwx（读写执行）
   ```
   chmod go-rw <file>
   # 修改文件所有者
   sudo chown <user> <file>
   ```

#### 新建

1. `touch`是更改已有文件的时间戳，但其在不加任何参数的情况下，只指定一个文件名，则可以创建一个指定文件名的空白文件（不会覆盖已有同名文件）

#### 复制

```
cp <file> <dr>
# 复制目录需要递归
cp -r <dr> <dr>
```

#### 删除

```
rm <file> 
# 删除目录需要递归
rm -r <dr> 
```

#### 移动

```
mv <file> <dr>
```

#### 重命名

```
mv <file> <newname>
# 批量重命名
rename <正则表达式> 
```
