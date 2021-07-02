[添加修改——本地仓库](#添加修改——本地仓库)  
[添加修改——远程仓库](#添加修改——远程仓库)  
[更改远程仓库](#更改远程仓库)  
[将本地仓库关联并推送到远程库](#将本地仓库关联并推送到远程库)  


#### 添加修改——本地仓库

1\. 查看状态
```
git status
```

2\. 添加所有修改文件到暂存区
```
git add .
```

3\. 提交到本地仓库
```
git commit -m 'xxx'
```

4\. 查看状态
```
git status
```

----

#### 添加修改——远程仓库

```
git push
```

----

#### 更改远程仓库  
> 针对报错 `fatal: remote origin already exists.`。  

1\. 删除远程 Git 仓库
```
git remote rm origin
```

2\. 添加远程 Git 仓库
```
git remote add origin https://github.com/SpringLoach/manager-copy.git
```

----

#### 将本地仓库关联并推送到远程库

1\. 新建空的远程库

2\. 在项目文件下执行如下命令
> 其中 `manager-copy` 为远程库名称，`main` 为分支名，`SpringLoach` 为 GitHub 账号。  
```
git remote add origin https://github.com/SpringLoach/manager-copy.git
git branch -M main
git push -u origin main
```
