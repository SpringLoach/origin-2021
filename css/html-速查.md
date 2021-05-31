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
> 如果不定义边框属性，表格将不显示边框。
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

 标签 | 说明
 :-: | :-: 
 <table\> | 定义表格
 <tr\> | 定义表格行
 <th\> | 定义表头，可选
 <td\> | 定义单元格

 属性 | 使用标签 | 说明
 :-: | :-: | :-: 
 cellpadding | <table\> | 增加各单元格的内边距
 cellspacing | <table\> | 增加各单元格边框间的间距
 width | <table\> | 规定表格的总宽度
 align | <table\>、<tr\>、<td\> | 规定表格单元内容的排列顺序  
 frame | <table\> | 规定围绕表格的边框

:herb: 对表格添加样式 `border-collapse: collapse;` 规定将表格边框折叠为单一边框，更多样式可以[查阅文档](https://www.w3school.com.cn/css/css_table.asp)。  

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

  标签 | 功能 | 说明
  :-: | :-: | :-: 
  <form\> | 定义表单 | 必填
  <fieldset\> | 组合表单中的相关数据 | 可选
  <legend\> | 为 `<fieldset>` 定义标题 | 可选
  <input type="text"\> | 定义用于文本输入的单行输入字段 | `value` 定义默认文字
  <input type="radio"\> | 定义单选按钮输入 | 同处单选按钮的 `name` 相等，需设置 `value` 用于提交
  <input type="checkbox"> | 定义复选框 | 同处复选框的 `name` 相等，需设置 `value` 用于提交
  <input type="submit"\> | 定义用于向**表单处理程序**提交表单的按钮 | `value` 定义默认文字
  <input type="password"> | 定义密码字段 | 字段中的字符会被做掩码处理
  <select\>| 定义下拉列表 | 该处规定 `name` 属性
  <option\> | 定义下拉列表中待选择的选项 | 该处规定 `value` 属性
  <textarea\> | 定义多行输入字段 | 标签中的文本为默认文字，`rows` 和 `cols` 可以定义文本框大小
  <button type="button"\> | 定义可点击的**按钮** | 经常添加 `onclick` 属性


  <datalist\> | 为 `<input>` 元素规定预定义选项列表 | `<input>` 的 list 属性必须引用 `<datalist>` 的 id 属性，在 `<datalist>`内部使用 `<option>`来添加预定义选项

  HTML5 增加了多个新的[输入类型](https://www.w3school.com.cn/html/html_form_input_types.asp)，用于图形化给用户提供选择颜色、日期等选项，可以添加属性进行输入限制并进行验证。

```
<form action="action_page.php">
<input list="browsers">
<datalist id="browsers">
   <option value="Internet Explorer">
   <option value="Firefox">
   <option value="Chrome">
   <option value="Opera">
   <option value="Safari">
</datalist> 
</form>
```


 属性 | 使用标签 | 说明 | 版本
 :-: | :-: | :-: | :-: 
 action | <form\> | 指定表单的处理程序 | /
 method | <form\> | 规定在提交表单时所用的 HTTP 方法（GET 或 POST） | /
 target | <form\> | 规定提交表单后在何处显示响应 | /
 autocomplete | <form\> | 值为 `on` 时规定根据用户之前输入的值自动填写值 | /
 novalidate | <form\> | 布尔值，规定提交时是否应验证表单数据 | /
 name |  所有表单元素 | **如果表单元素需要提交**，必须设置一个 name 属性 | /
 selected | <option\> | 布尔属性，定义预定义选项 | /
 value | <input\>等 | 规定输入字段的初始值 | /
 readonly | <input\> | 布尔属性，规定输入字段为只读 | /
 disabled | <input\> | 布尔属性，规定输入字段是禁用的，不会被提交 | /
 size | <input\> | 规定输入字段的尺寸（以字符计） | /
 maxlength | <input\> | 规定输入字段允许的最多数量 | /
 autocomplete | <input\>、<form\> | 规定表单或输入字段是否应该自动完成 | HTML5 



----
### 字符实体  

符号|a
 :-: | :-: 
<|&lt  
\>|&gt  
©|&#169  
空格|$nbsp;  

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






