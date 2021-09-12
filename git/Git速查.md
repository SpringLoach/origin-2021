<details>
  <summary>展开手册</summary> 

操作 | 指令 | 别名 | 说明  
:- | :- | :- | :-
初始化仓库 | git init | / | 使用其它指令的前提  
添加文件到缓存区 | git add <file\> | / | 可反复多次使用   
将缓存文件提交本地仓库 | git commit -m <message\> | / | /  
查看分支 | git branch | / | /
创建分支 | git branch <name\> | / | /
切换分支 | git checkout <name\> | git switch <name\> | / 
创建+切换分支 | git checkout -b <name\> | git switch -c <name\> | / 
合并某分支到当前分支 | git merge <name\> | / | 需要先切换到当前分支  
删除分支 | git branch -d <name\> | / | /  
强行删除分支 | git branch -D <name\> | / | 分支未合并过时，不能普通删除
前往某次提交版本 | git reset --hard <commit_id\>  | / | /
查看提交历史 | git log  | / | 方便回到过去版本
查看命令历史 | git reflog  | / | 方便前往未来版本  
丢弃工作区修改 | git checkout -- <file\> | / | 尚未添加到缓存
丢弃缓存区修改 | git reset HEAD <file\> | / | 需要再执行上一步 
从版本库恢复被删除文件 | git checkout -- <file\> | / | 需要版本库存在该文件   
从版本库恢复被修改文件 | git checkout -- <file\> | / | 需要版本库存在该文件   
从版本库删除文件 | git rm <file\> | / | 需要提交操作  
关联远程库 | git remote add origin <url.git\> | / | origin 是远程库的习惯命名  
推送当前分支到远程**并关联** | git push -u origin <name\> | / | 关联当前、远程分支，后续推送/拉取可以简化命令  
↑ | / | / | 如远程分支不存在，将新建远程分支
将当前分支推送（更新）到远程 | git push origin <name\> | / | 分支通常重名  
将当前分支推送（更新）到远程 | git push origin | / | 需要关联当前、远程分支  
将当前分支推送（更新）到远程 | git push | / | 还需要当前分支只有一个远程分支   
从远程库克隆 | git clone <url.git\> | / | /
查看远程库信息 | git remote -v | / | /
建立远程的某分支到本地 | git checkout -b <branch\> origin/<branch\> | / | 应该不需要下一步
关联本地、远程分支 | git branch --set-upstream-to <branch\> origin/<branch\> | / | /
合并本地、远程分支 | git pull | / | 远程分支比本地更新时使用。需要先关联
  
  
</details> 




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
  
----

#### 提交用户信息  
> 添加 `--global` 参数，表示机器上所有的Git仓库都会使用这个配置。  
  
```  
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"  
```
  
  
  
