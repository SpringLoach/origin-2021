## 使用Git  
> Git 是目前世界上最先进的分布式版本控制系统

**下载安装Git**  
　　Git官网下载：https://www.git-scm.com/download/win
  
**操作方法**  
　　- **Git Bash**：Unix 与 Linux 风格的命令行模式，**推荐使用**  
　　- **Git CMD**：Windows 风格的命令行  
　　- **Git GUI**：图形界面  

## 基本信息设置

> 确认/验证贡献者的信息，会在仓库主页显示

**设置用户名**  
`git config --global user.name 'nameVal'`    
栗子  
`git config --global user.name 'superman'`  

**设置用户邮箱**  
`git config --global user.email 'email@qq.com'`   
栗子   
`git config --global user.email '123504842@qq.com'`

## 本地仓库的操作

> 在选定的文件夹中 → 右键 → **Git Bash Here**

### 创建一个合适的git仓库  
**命令行创建新的文件夹**  
`mkdir 文件夹名`  

**进入某文件夹中**  
`cd 文件名`

**初始化 Git（创建Git仓库，用于存储本地仓库信息）**  
`git init`  
> 创建一个隐藏文件  

### 向仓库添加文件  
1. **创建文件**  
```
touch 文件名
```  
> 文件名要有后缀  
  
2. **将文件移动——工作区 → 暂存区**  
```
git add 文件名
```  
  
3. **将文件移动——暂存区 → 本地Git仓库**  
```
git commit -m '描述内容'
```

### 修改仓库文件
`vi 文件名`  
> 按 `i` 切换到插入模式。  
> 完成后，Shift + zz　退出  
> 修改成功后，修改后的文件仍在 **工作区**，需要移动到暂存区 → Git 仓库

### 删除仓库文件 
1. **删除文件**  
```
rm -rf 文件名
```  
> 程序员**禁忌**，最好别用
  
2. **从 Git 删除文件**  
```
git rm 文件名
```  
  
3. **提交操作**  
```
git commit -m '描述内容'
```  
> 增删改**都需要**提交  

## 管理远程仓库

> 备份；实现代码共享集中化管理

**克隆远程仓库到本地**  
`git clone 仓库地址`   
> **如果克隆失败**，将 https 改为 git．
> 然后在推送前修改远程 Git 仓库地址　`git remote set-url origin 仓库地址`

**修改，上传到本地仓库**

**将本地仓库同步到 git 远程仓库**  
`git push`

## 其他命令

**查看状态**
`git status`

**查看当前文件**
`ls`

**回到上一级**
`cd ..`

**进入指定文件**
`cd 相对路径的文件名`

**显示当前所在的目录路径**
`pwd`

**清屏**
`clear`

**列出当前目录中的所有文件**
`ls`
> 绿色：程序 紫色：目录(文件夹) 白色：文件


**添加所有文件到缓存区**
`git add .`

**删除文件**
`rm 文件名`

**删除文件夹**
`rm -r 文件夹名`

**切勿在Linux中尝试**
`rm -r 后面加f加空格加/`,这将清空电脑中的全部文件

**移动文件**
`mv 文件名 文件夹`

**查看历史命令**
`history`

**退出Git Bash**
`exit`

**注释**
`#`

## Git 配置

**查看配置**
`git config -l`

**查看系统配置（不会显示用户配置）**
`git config --system --list`

**查看用户配置**
git config --global --list

### Git 相关的配置文件：  
- system系统级  
`Git\etc\gitconfig`（ Git 安装目录下 ）  
- global 全局  
`C:\Users\Administrator\gitconfig` ( 需先配置 ）

## 分支命令

**列出所有分支**
`git branch`

**列出所有远程分支**
`git branch -r`

**新建一个分支，但仍停留在当前分支**
`git branch 分支名      （没有后缀）`

**新建一个分支，并切换到该分支**
`git checkout -b 分支名`

**合并指定分支到当前分支**
`git merge 分支名`

**删除分支**
`git branch -d 分支名`

**删除远程分支**
`git push origin --delete 分支名`











