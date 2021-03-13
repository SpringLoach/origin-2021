## 分支管理  
> 在不影响主分支正常使用的前提下，在另外一条自己的分支上干活（任意提交），最后开发完毕后，再一次性合并到原来的分支上。

## 创建与合并分支（图解部分）

HEAD 严格来说不是指向提交，而是指向 *master( 主分支 )*， *master* 才是指向提交的，所以，**HEAD 指向当前分支**。
每次提交，*master* 分支都会向前移动一步，这样，随着你不断提交，*master* 分支的线也越来越长。  
　　![分支1](分支1.png)

1. 创建新分支 *dev* 并改变指向：  
![分支2](分支2.png)

2. 此后，对**工作区的修改和提交**就是针对 *dev* 分支了。  
   接下来我们进行提交一次：  
![分支3](分支3.png)

3. 完成合并：把 *master* 指向 *dev* 的 **当前提交**：  
![分支4](分支4.png)

4. 合并完分支后，甚至可以删除 *dev* 分支（ 即 *dev* 指针）。  
![分支5](分支5.png)

## 创建与合并分支（实战部分）

**创建新分支 *dev* 并改变指向：**  
```
$ git switch -c dev
```  

可以用 `git branch` 命令**查看当前分支**( 列出所有分支，其中 `*` 指向当前分支 )：
```
$ git branch
* dev
  master
```

**在 *dev* 分支上完成一次修改和提交后**

**切换回 *master* 分支**  
> 到这里，是没有之前在 *dev* 分支的提交的。
> 
> 一般都是提交后，再切分支，用以避免缓存区的混乱。
```
$ git switch master
```  

**把 *dev* 分支的工作成果 合并 到 *master* 分支上**  
```
$ git merge dev
```  
会被告知 **Fast-forward** 的信息，代表“快进模式”，也就是直接把 *master* 指向 *dev* 的**当前提交**。

**删除 *dev* 分支**  
```
$ git branch -d dev
```  

### 旧版本使用的命令  
**创建新分支 *dev* 并改变指向：**  
```
$ git checkout -b dev
```  
`git checkout` 命令加上 `-b` 参数表示创建并切换，相当于以下两条命令：  
```
$ git branch dev
$ git checkout dev
```

**直接切换到已有的 *master* 分支**  
```
$ git checkout master
``` 

## 解决冲突（图解部分）  
当我们对新建的 *feature1* 分支和 *master* 分支**分别有新的提交**时，Git 将无法执行“ 快速合并 ”，只能试图把各自的修改**合并**起来，但这种合并就可能会有**冲突**。  
　　![分支2.1](分支2.1.png)  
此时，需要手动解决冲突后 **再提交**。提交后，*master* 分支和 *feature1* 分支变成了下图所示：  
　　![分支2.2](分支2.2.png)  
最后，删除 *feature1* 分支，工作完成。  

## 解决冲突（实战部分）  
**在两个分支分别有新的提交后，尝试合并：**  
```
$ git merge feature1
Auto-merging a.html
CONFLICT (content): Merge conflict in a.html
Automatic merge failed; fix conflicts and then commit the result.
```  
Git 返回信息：*a.html* 文件存在冲突，必须手动解决冲突后再提交。  
> 通过 `git status`，可以查看冲突的文件。  
> 同时它告诉我们当前 *master* 分支比**远程**的 *master* 分支要超前 2 个提交：
>```
> $ git status
> On branch master
> Your branch is ahead of 'origin/master' by 2 commits.
> ......
> both modified:   a.html
> ```

**手动解决冲突**  
> Git 用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。

**再提交**  
```
$ git add a.html 
$ git commit -m "miaoshu"
```  
> 用 `git log --graph` 可以看到分支的合并情况。  
> 此时 *master* 在同分支下领先于 *feature1* 一个提交，若再合并就是“ 快速合并 ”。

**最后，删除 *feature1* 分支**  










