## 下载安装Git

　　Git官网下载：https://www.git-scm.com/download/win
  
**操作方法：**  
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











