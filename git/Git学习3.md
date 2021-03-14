## 创建标签  
> 将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。  
> *tag* 就是一个让人容易记住的有意义的名字，它跟某个 *commit* 绑在一起。  

#### 创建默认标签  
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

## 查看标签

#### 查看所有标签  
> 注意，标签不是按时间顺序列出，而是按字母排序的。  
```
$ git tag
```

#### 查看标签信息   
```
git show <tagname>
```  

## 删除标签   
> 因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。  

#### 删除某个本地标签  
```
$ git tag -d <tagname>
```
#### 删除已经推送到远程的标签  
- **先从本地删除**   
```
$ git tag -d <tagname>
```  
- **再从远程删除**
> 注意 origin 和冒号之间有个**空格**， 相当于 push 一个空的 *tag* 到远程。
```
$ git push origin :refs/tags/<tagname>
```

## 推送标签  
#### 推送某个标签到远程  
```
git push origin <tagname>
```  

#### 推送全部尚未推送到远程的本地标签  
```
$ git push origin --tags
```





