## 分支管理  
> 在不影响主分支正常使用的前提下，在另外一条自己的分支上干活（任意提交），最后开发完毕后，再一次性合并到原来的分支上。

## 创建与合并分支（图解部分）

HEAD 严格来说不是指向提交，而是指向 *master( “主”分支 )*， *master* 才是指向提交的，所以，**HEAD 指向当前分支**。
每次提交，*master* 分支都会向前移动一步，这样，随着你不断提交，*master* 分支的（ 时间 ）线也越来越长。  
　　![分支1](分支1.png)

1. 创建新分支 *dev* 并改变指向：  
![分支2](分支2.png)

2. 此后，对**工作区的修改和提交**就是针对 *dev* 分支了。  
   接下来我们进行提交一次：  
![分支3](分支3.png)

3. 完成合并：把 *master* 指向 *dev* 的 **当前提交**：  
![分支4](分支4.png)

4. 合并完分支后，甚至可以删除 *dev* 分支（ 本质即 *dev* 指针）。  
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

## 分支管理策略  

### 普通模式合并
合并分支时，加上 `--no-ff` 参数( 表示禁用`fast forward` )就可以用普通模式合并。  
```
$ git merge --no-ff -m "miaoshu" dev
```  
　　![分支3.1](分支3.1.png)

**普通模式 VS 快速合并**  
普通模式合并后的历史有分支，会在 `merge` 时生成一个新的 **commit**，能看出来曾经做过合并。  
而 `fast forward` 合并就看不出来曾经做过合并，删除分支后，会丢掉分支信息。

### 分支策略  
> 在实际开发中，我们应该按照几个基本原则进行分支管理。  

- *master* 分支应该是非常稳定的，也就是仅用来发布新版本。  
- 干活都在 *dev* 分支上，在版本发布时（如1.0），再把 *dev* 分支合并到 *master* 上，在 *master* 分支发布 1.0 版本。  
- 大家都在 *dev* 分支上干活，每个人都有**自己的分支**，时不时地往 *dev* 分支上合并。  
　　![分支3.2](分支3.2.png)

## Bug 分支  
> 修复 bug 时，我们会通过创建新的 bug 分支进行修复，然后合并，最后删除。

**储藏现场**  
> 工作到一半，被告知要紧急修复一个 bug，此时在分支 dev 上进行的工作还没提交（ 包括未 `git add` ）。  
```
$ git stash
```  

**然后切换到修复 bug 的分支上（ 如 *master* 分支），创建新的 bug 分支进行修复，然后合并，最后删除。**

**在其他分支修复同样的 bug**
> 切换回 *dev* 分支后，突然想到，*dev* 分支是早期从 *master* 分支分出来的，故这个 bug 其实在当前 *dev* 分支上 **也存在**。  
> 
> 除了可以重复操作提交外，还可以：  
```
$ git cherry-pick 4c805e2
```  
> 其中的 `4c805e2` 代表先前修复 bug 的提交。  
>```  
> $ git add a.html   
> $ git commit -m "fix bug 101"  
> [issue-101 4c805e2] fix bug 101  
>  1 file changed, 1 insertion(+), 1 deletion(-)  
> ```  

当然，也可以先在 *div* 分支保存现场，待修复 bug 后，在到 *master* 分支上“ 重放 ”修复。

### 回到工作现场  
> 此时的工作区是干净的，刚才的工作现场可以用 `git stash list` 命令看看。  
> ```
> $ git stash list  
> stash@{0}: WIP on dev: f52c633 add merge  
> ```  
> 
**恢复现场**
- 方法一：用 `git stash apply` 恢复，但是恢复后，stash 内容并没有删除，需要用 `git stash drop` 来删除。
- 方法二：用 `git stash pop`，恢复的同时把 stash 内容也删。

> **多次储藏**  
> 可以多次 stash，恢复的时候，先用 `git stash list`查看，然后恢复**指定的 stash**，用命令：  
> ```
> $ git stash apply stash@{0}
> ```  
 
### 注意事项  
- 也可以先将工作现场的任务完成 **提交后**，再“ 重放 ”修复。
- 如果修复 bug 与工作现场的修改在同个文件的相同处，“ 重放 ”修复可能会导致报错。

## Feature分支  
> 添加一个新功能时，肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个 *feature* 分支，在上面开发，完成后，合并，最后，删除该 *feature* 分支。这个过程类似于 *处理 bug*。

**强行删除**  
> 准备合并分支前，突然被告知：新功能取消，这个包含新功能的 *feature* 分支 **必须销毁**。 
> 
> 其中的 *feature-121* 为分支名称  
```
$ git branch -D feature-121               
```  
> tip：没有合并过的分支，如果删除，将 **丢失修改**，普通的方法去删除分支会被报错：  
> ```
> $ git branch -d feature-121
> error: The branch 'feature-121' is not fully merged.
> If you are sure you want to delete it, run 'git branch -D feature-121'.
> ```  
> （ 正常工作中，为了防止需求变动，不会直接这么操作吧？）





