
### 个人中心

#### 个人中心_动态渲染信息区  

步骤 | 说明 | 解释
:-: | :-: | :-   
动态渲染 | 判断逻辑 | 根据缓存中是否有个人信息，条件渲染不同的内容
获取信息 | 先前方法 | 跳转到登录页，并提供一个获取个人信息类型的 `<button>`。将数据保存到缓存和页面后，返回先前页面  
获取信息 | 实际可以 | 可以通过点击触发 [wx.getUserInfo](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/user-info/wx.getUserInfo.html) 获取个人信息
获取信息 | 其它说明 | 信息中包括头像、用户名等  



子绝父相，想要居中对齐时，还是使用 `left: 50%;`和 `transform: translateX(-50%);` ，可以设置百分比宽度来实现两边空隙  
使用 `nth-last-of-type()` 时，需要注意选项是否在同一个容器下，而不是在各自的容器中。  











