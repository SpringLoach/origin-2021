## 创建标签  
> 将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。  
> *tag* 就是一个让人容易记住的有意义的名字，它跟某个 *commit* 绑在一起。  

### 默认标签  
> 首先切换到需要打标签的分支上，标签会打在最新提交的 *commit* 上。
> 
> \<name\>可以输入 v1.0
```
$ git tag <name>
```

#### 对指定的 commit 打标签  
> \<id\>需要输入指定的 **commit id**。
```
$ git tag <name> <id>
```  
**注意：标签总是和某个 *commit* 挂钩。如果这个 *commit* 既出现在 *master* 分支，又出现在 *dev* 分支，那么在这两个分支上都可以看到这个标签。**

> 查找历史提交的commit id  
> ```
> $ git log --pretty=oneline --abbrev-commit
> ```

#### 创建带有说明的标签   
> 用 `-a` 指定标签名，`-m` 指定说明文字  
```
$ git tag -a <name> -m "miaoshu" <id>
```  
----

#### 查看所有标签  
> 注意，标签不是按时间顺序列出，而是按字母排序的。  
```
$ git tag
```

#### 查看标签信息   
```
git show <tagname>
```  




