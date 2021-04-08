## 目录  
[基本文档](#基本文档)  
[文本元素](#文本元素)   
[实体样式](#实体样式)  
[链接与锚](#链接与锚)  
### 列表 
- [无序列表](#无序列表)  
- [有序列表](#有序列表)  
- [定义列表](#定义列表)   

[表格](#表格)  
[表单](#表单)  
[字符实体](#字符实体)  
[框架](#框架)  
[逻辑样式](#逻辑样式)  
[其他元素](#其他元素)  

----
### 基本文档
```
<html>
<head>
<title>文档标题</title>
</head>
<body>
Visible text goes here
</body>
</html>
```

----
### 文本元素  
```
<p>段落</p>
<br>  换行
<hr>  水平线
<pre>预格式化了的文本</pre>
```

----
### 实体样式
```
<b>加粗</b>
<i>斜体</i>
```

----
### 链接与锚  
```
<a href="http://www.example.com/">链接提示</a>

<a href="http://www.example.com/"><img src="URL" alt="替代文本"></a>

<a name="tips">目的地</a>
<a href="#tips">按我起飞</a>

<a href="mailto:webmaster@example.com">Send e-mail</a>A named anchor:
```

----
### 无序列表  
```
<ul>
    <li>第一项</li>
    <li>第二项</li>
</ul>
```

----
### 有序列表  
```
<ol>
    <li>第一项</li>
    <li>第二项</li>
</ol>
```

----
### 定义列表  
```
<dl>
    <dt>第一项</dt>
        <dd>定义内容</dd>
    <dt>第二项</dt>
        <dd>定义内容</dd>
</dl>
```

----
### 表格    
```
<table border="1">
<tr>
    <th>标题一</th>
    <th>标题二</th>
</tr>
<tr>
    <td>一些内容</td>
    <td>一些内容</td>
</tr>
</table>
```

----
### 表单
> 需要补充。  
```
<form action="http://www.example.com/test.asp" method="post/get">  // 提交表单到服务器的文件 & 提交表单时所用的 HTTP 方法
<input type="text" name="lastname"                                 // 如果要正确地被提交，每个 输入字段 必须设置一个 name 属性。
value="Nixon" size="30" maxlength="50">                            // 定义供文本输入的单行输入字段
<input type="password">                                            // 定义密码字段
<input type="checkbox" checked="checked">
<input type="radio" checked="checked">
<input type="submit" value="点击提交">                              // 定义提交的按钮
<input type="reset">
<input type="hidden">
<select>                 // 下拉列表
<option value="f1">苹果</option>  // 定义待选择的选项
<option value="f2">香蕉</option>
<option value="f3">西瓜</option>
</select>
<textarea name="Comment" rows="60"    // 定义多行输入字段（文本域）
cols="20"></textarea>
</form>
```
> value 属性规定输入字段的初始值  
> size 属性规定输入字段的尺寸（以字符计）  
> maxlength 属性规定输入字段允许的最大长度  

----
### 字符实体  

符号|a
 :-: | :-: 
<|&lt  
\>|&gt  
©|&#169  

----
### 框架  
```
<frameset cols="25%,75%">
    <frame src="页面1.htm">
    <frame src="页面2.htm">
</frameset>
```

----
### 逻辑样式
```
<em>强调的部分</em>    // 表现为斜体
<strong>强的语气</strong>  // 表现为加粗
<code>computer code</code>
```

----
### 其他元素
```
<!-- 一些备注 -->
<blockquote>引用的内容</blockquote>
```






