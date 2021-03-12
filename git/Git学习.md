## 简介  
> Git 是最强大的分布式版本控制系统，没有之一。想要多人一起合作完成项目，学习 Git 是非常有必要的。以下是一些自己的学习笔记，主要参考自[廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)。

## 安装 Git  
> 在 Windows 上使用 Git，可以从 Git 官网直接下载安装程序，然后按默认选项安装即可。

安装好后，每个机器需要自报家门：  
```
$ git config --global user.name "Your Name"
```  
```
$ git config --global user.email "email@example.com"
```  
注意 `--global` 参数，表示该机器的所有 Git 仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 创建版本库  
> 版本库又名仓库，英文名 repository，可以简单理解成一个目录。Git 可以管理目录里面的所有文件，甚至任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

创建一个版本库，需要在合适的地方创建一个空目录
```
$ mkdir 文件夹名
$ cd 文件夹名
$ pwd
/将会出现当前目录
```
`pwd` 命令用于显示当前目录。  
**使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。**  
然后，通过 `git init` 命令把这个目录变成Git可以管理的仓库:  
```
$ git init
Initialized empty Git repository in 当前目录/.git/
```
可以使用 `ls -ah` 命令查看隐藏的.git目录

### 把文件添加到版本库  
> 编写的文件，要放到当前目录下（或它的子目录），确保它放到了 Git 仓库中。

首先，用命令 `git add`，把文件添加到仓库：  
```
$ git add 加后缀的文件名
```  
然后，用命令 `git commit`，把文件提交到仓库：  
```
$ git commit -m "提交说明"
[master (root-commit) eaadf4e] xxxx
 1 file changed, 2 insertions(+)
 create mode 100644 文件名 
```  
执行成功后，告知：`1 file changed`: 1个文件被改动;`2 insertions`：插入了两行内容。

要知道 commit 可以一次提交很多文件，所以可以**多次 add 不同的文件**：  
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

### 注意事项  
Git 命令必须在 **Git 仓库目录内**执行（git init 除外），在仓库目录外执行是没有意义的。  
添加某个文件时，该文件必须在当前目录下**存在**（ 有时会不小心写错文件名 ），可以用 `ls` 命令查看当前目录的文件。  

所有的版本控制系统（包括 Git），其实**只能跟踪文本文件的改动**，比如 TXT 文件，网页，所有的程序代码等等；对于（二进制文件）图片、视频、Word，只能知道大小的变化，没法跟踪。  
因为文本是有编码的，建议使用标准的 *UTF-8编码* 。  
**Windows** 的记事本  
不要使用 Windows 自带的记事本编辑任何文本文件，会遇到很多不可思议的问题，建议下载 [Notepad++](http://notepad-plus-plus.org/) 代替记事本。  
Unix 的哲学是“ 没有消息就是好消息 ”。






