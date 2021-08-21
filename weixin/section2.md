
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

### 订单查询  

#### 订单查询_跳转请求数据  

步骤 | 说明 | 解释
:-: | :-: | :-   
① | 跳转到页面 | 在我的页面通过 `<navigator url="">`，携带参数跳转
② | 选择钩子 | 由于该页面使用频率较高，故选择在 `onShow` 中请求数据等
③ | 获取令牌 | 由于请求列表数据需要 `token`，先判断缓存有无 `token`，无就请求得
④ | 获取参数 | 该钩子中，需要通过  `getCurrentPages()`，获取页面栈，取其返回数组的最后项的 `options`
⑤ | 传递索引 | 保存当前激活索引，传递给子组件用于标题的激活样式
⑤ | 获取数据 | /
⑥ | 获取数据 | 在点击回调中，请求相对应的数据  

```
onShow: function () {
  // 从页面栈中获取所需页面参数 type
  const pagesArr = getCurrentPages();
  let {type} = pagesArr[pagesArr.length-1].options;
}
```

#### 订单查询_处理时间戳  

```
// res.orders 为请求到的目标数组
let listData = res.orders.map(item => {return {...item, create_time_treat: new Date(item.create_time*1000).toLocaleString()}} )
this.setData({
  listData
})
```

----

#### 详情页_收藏功能  
> 由于后端没有提供相应的接口，只能临时靠缓存实现。  

步骤 | 说明 | 解释
:-: | :-: | :-   
① | 钩子切换 | 猜测是考虑到从收藏页切回详情页的情况，将先前的请求[等逻辑](#订单查询_跳转请求数据)也放到了 `onShow`
② | 钩子切换 | 因为判断收藏情况需要用到商品详情数据和缓存的收藏数据，将逻辑放在请求数据后
③ | 动态渲染 | 动态渲染需要的 `icon`
④ | 点击回调 | 缓存中没有时，将商品数据添加到缓存
⑤ | 点击回调 | 否则，从缓存中移除该商品数据
⑤ | 点击回调 | 动态渲染需要的 `icon`

#### 个人中心_显示收藏数量  
> 在钩子中获取缓存保存到页面，渲染即可。同时添加链接。  

#### 收藏页  
> 缝合怪。  

### 搜索页  

#### 搜索页_基础布局  
> 注意 `<button>` 的样式，需要通过类名设置，且它的一些默认属性干扰很大（如 `size` 会影响字体的横向排布）。  

#### 搜索页_搜索实现  
> 当用户输入完毕后，点击搜索才出现相应搜索信息，也许并不是一个好的体验。  
> 
> 注意 `<input>` 的 `value` 属性，本身只能决定初始值而没有绑定值。  

步骤 | 说明 | 解释
:-: | :-: | :-   
① | 搜索实现 | 本质是将关键词发送给后端，取得相应数据进行渲染
② | 搜索实现 | 验证输入值后，即有无实际内容。通过后发起请求
③ | 清空功能 | 需要将输入值保存到本地
④ | 清空功能 | 再将输入值通过赋值到 `value` 属性上
⑤ | 清空功能 | 清除数据，重置初始值
⑤ | 防抖功能 | 微实现很简单  

```
<input placeholder=".." bind:input="handleInput" value="{{inputValue}}"></input>
<button size="mini" bind:tap="clickClean">清空</button>

data: {
  inputValue: '',
  searchData: []
},
timer: null,
clickClean() {
  this.setData({
    inputValue: '',
    searchData: []
  })
},
handleInput(e) {
  let inputValue = e.detail.value;
  this.setData({
    inputValue
  })
  // 验证有效性  
  if(!inputValue.trim()) {
    return
  }
  // 防抖版请求数据 
  clearTimeout(this.timer);
  this.timer = setTimeout(() => {
    this.getSearchData(inputValue);
  }, 800)
},
getSearchData(query) {
  getSearchData({data: {query}}).then(res => {
    this.setData({
      searchData: res.splice(0,10)
    })
  })
}
```

























