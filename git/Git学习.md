## 简介  
> Git 是最强大的分布式版本控制系统，没有之一。想要多人一起合作完成项目，学习 Git 是非常有必要的。以下是一些自己的学习笔记，主要参考[廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)。

## 安装 Git  
> 在 Windows 上使用 Git，可以从 Git 官网直接下载安装程序，然后按默认选项安装即可。

安装好后，每个机器需要自报家门：  
``
$ git config --global user.name "Your Name"
``  
``
$ git config --global user.email "email@example.com"
``  
注意 `--global` 参数，表示该机器的所有 Git 仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
