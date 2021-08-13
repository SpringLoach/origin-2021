#### 起步

1. 申请[账号](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#申请帐号) ，需要提供邮箱、管理员用微信扫码。  

2. 在[小程序后台](https://mp.weixin.qq.com/)，（开发管理-开发设置）可以获取 AppID，其相当于小程序的身份证，调用某些接口需要用到它。  

3. 安装[开发工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)，用于预览效果。编写代码可以用 VS Code。  

4. 对于测试功能，打开开发工具后，创建小程序，**选择一个空目录**，使用测试号，即可实现第一个小程序。 

5. 后期可以打开项目后，在 `详情` 修改 AppId。  

#### 目录结构

小程序文件结构

类型 | 传统web | 微信小程序
:-: | :-: | :-: 
结构 | HTML | WXML 
样式 | CSS | WXSS
逻辑 | Javascript | Javascript
配置 | 无 | JSON

![结构目录](./img/结构目录.png)

文件 | 说明
:-: | :-: 
project.config.json | 也可以在 `详情` 的 UI 界面进行设置 

#### app.json  
> 用来对微信小程序进行全局配置，决定页面文件的路径、窗口表现、设置网络超时时间、设置多 tab 等。  
>
> 小程序页面也可以使用同名 `.json` 文件（仅能）对窗口表现进行配置，会覆盖全局的 `window` 中相同的配置项。
>
> 使用开发者工具进行配置时，会有相应字段的提示和补全功能。  

pages字段    
> 决定页面文件的路径。  

1. 每个数组元素都对应着一个页面的路径，最后项不需要后缀名。  

2. 使用开发工具，在该选项下新增元素并保存，会自动生成对应的页面文件。  

3. 首个数组元素对应的路径将展示为首页。  

window字段  
> 定义小程序所有页面的顶部背景颜色，文字颜色等。  

常用属性 | 说明 | 默认值 | 可选值
:- | :- | :- | :-
navigationBarBackgroundColor | 导航栏背景颜色 | "#fff" | *HexColor*
navigationBarTitleText | 导航栏标题 | "Weixin" | *str*
navigationBarTextStyle | 导航栏标题颜色 | "black" | "white"
backgroundTextStyle | 下拉加载，指示器颜色 | "dark" | "light"
enablePullDownRefresh | 开启当前页面下拉刷新 | false | true
backgroundColor | 下拉加载部分窗口颜色 | "#ffffff" | *HexColor*




