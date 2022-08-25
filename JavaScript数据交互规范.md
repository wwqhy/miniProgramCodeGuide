#### 一、使用指向page自身的this
在每个页面逻辑`.js`文件里全局声明`that`，在`Page()`函数的参数`onLoad`方法内把`this`赋给`that`
```
let that;
Page({
  ...
  onLoad: function () {
    that = this;
  }
  ...
})
```

#### 二、来源页面

> 当小程序功能增多，业务变得复杂，页面间的相互跳转也会更加频繁。从不同的来源页面跳转到同一个目标页面时，前者可能会要求后者差异化显示内容或进行不同的数据操作。后者则需要根据某种方式来区分不同的来源页从而进行相应的数据处理。

###### 团队约定
 
使用`navigator`组件或导航相关API时，`url`必带一个参数`f`，参数`f`值为来源页面的名称。目标页面通过参数`f`来区分来源页面。
```
// 从动态列表 event_list 进入个人主页 personal_page 

/* WXML */
<navigator url="/page/personal_page?f=event_list">跳转到新页面</navigator>

/* JavaScript */ 
wx.navigateTo({
  url: '/page/personal_page?f=event_list'
})
```

#### 三、网络请求(wx.request)

1. loading提示优化

    loading提示能让用户知道当前的操作进度，合理地显示loading提示，有助于提升产品气质和用户体验。

    > 通常我们认为，发起请求即显示loading提示，请求完成隐藏loading提示。用户所处的网络环境较差时，loading提示会正常显示隐藏，用户所处网络环境良好时，loading提示会闪一下。大多时候用户所处的网络环境都是良好的，网络请求能即时返回结果，此时就没必要显示loading提示，也可以避免那尴尬的一闪。

    ###### 团队约定
    
    网络请求在800毫秒内返回了结果，不显示loading提示，超过800毫秒还未返回结果开始显示loading提示。
    
    ###### 实现思路
    
    在请求之前声明一个变量loadingStatus来控制loading提示何时显示。loadingStatus有以下两个值，分别代表二个状态：

    值 | 状态说明 | 是否显示loading提示
    --- | --- | ---
    -1 | 初始值 | 显示
    0  | 请求完成 | 不显示

    ```
    let loadingStatus = -1;
    ```
    
    在请求之前放置一枚定时器，这个定时器在800毫秒之后执行，在其内控制是否显示loading提示。

    ```
    /* 
    * 定时器在800毫秒后执行时，会判断loadingStatus状态，
    * 如果loadingStatus还是初始值-1（没有被改变过），就显示loading提示。
    * 如果loadingStatus不是-1，说明网络请求已返回（此时loadingStatus的值应该是0）。
    */
    setTimeout(() => {
      if (loadingStatus === -1) {
        wx.showLoading({
          title: '加载中...'
        })
      }
    }, 800);
    ```
        
    在`wx.request`参数的`complete`里改变loadingStatus的值
    
    ```
    wx.request({
        ...
        complete: function () {
            // 请求完成，改变loadingSataus的值
            loadingSataus = 0;
        }  
    })
    ```
    
    完整流程
    
    ```
      ...
      getUserInfo: function () {
        // 其它代码...
        let loadingStatus = -1;
        setTimeout(() => {
          if (loadingStatus === -1) {
            wx.showLoading({
              title: '加载中...'
            })
          }
        }, 800)
        // 开始请求
        wx.request({
          url: 'your api url',
          method: 'GET',
          data: {
            userid: 123456
          },
          success: function (res) {
            // 处理返回结果
          },
          fail: function () {
            // 处理失败 
          },
          complete: function () {
            // 请求完成，关掉loading，改变loadingSataus的值
            wx.hideLoading();
            loadingSataus = 0;
          }
        })
    
      },
      ...
    ```

2. 限制重复请求

    我们的程序里有很多个请求，某个网络请求在未完成的情况下，该请求不应该再被发起，必须加以限制，保证业务流程有序进行。尽管有些限制在后端处理了，但前端也必须加以限制，把隐患扼杀在摇篮。
    
    > 连续的重复请求不加限制，会让前端程序数据错乱（如列表类数据加载），也会给后端造成不必要性能的负担，甚至引起数据库数据错乱。如：签到，领取积分，点赞（听说手快能多点几个）。
    
    ###### 实现思路
    
    在全局声明一个`allowRequest`用来控制请求是否能再次发起。

    值 | 状态说明 | 是否允许发起请求
    --- | --- | ---
    -1 | 初始值，请求从未发起过| 允许
     0 | 正在请求中| 不允许
     1 | 请求完成| 允许
    ```
      onLoad: function () {
        /*
         * 当disabled为-1或1时可以再次发起网络请求，为0时不可发起。
         */ 
        this.allowRequest = -1;
      }
    ```
    在发起请求之前通过`allowRequest`判断是否能发起请求。
    ```
    // allowRequest值为0，表明已经有一个当前的请求在执行，不能再次发起请求，中断操作。
    if(that.allowRequest === 0) {
      return;
    }
    // 如果可以发起请求，发起之前把allowRequest值改为0
    that.allowRequest = 0;
    ```
    请求完成，在`wx.request`参数的`complete`里改变`allowRequest`的值
    ```
    // 其它代码...
    complete: function () {
      // 把allowRequest的值改为1
      allowRequest = 1;
    }
    ```
    完整流程
    ```
      ...
      onLoad: function () {
        this.allowRequest = -1;
      }
      ...
      getUserInfo: function () {
        let that = this;
        // 进入请求之前，检查是否可以发起网络请求
        if(that.allowRequest === 0) {
          return;
        }
        // 如果可以请求，就把disabled的值改成0
        that.allowRequest = 0;
        // 开始请求
        wx.request({
          url: 'your api url',
          method: 'GET',
          data: {
            userid: 123456
          },
          success: function (res) {
            // 请求成功的代码
          },
          fail: function () {
           // 请求失败的代码
          },
          complete: function () {
            that.disabled = 1;
          }
        })
      },
      ...
    ```
    
3. 请求错误处理

    不管网络请求返回错误`error`还是请求失败`fail`，都应该反馈给用户。
    
    > 部分开者开发过程中处理网络请求结果时，只处理请求成功返回成功的结果，而对返回错误和请求失败没做处理，这是不科学的。（数据没有请求成功，又不给用户对应的错误反馈，用户会一脸懵比的。）
    
    ###### 团队约定
    
    为了方便开者准确定位错误和更舒适的用户体验，每个网络请求必须处理请返回错误`error`和请求失败`fail`，并适当地反馈给用户。
    
    `wx.request`参数的`fail`方法必须写法。
    ```
    getUserInfo: function () {
      ...
      wx.request({
        url: api.host + '/YinianProject/points/showPersonInfo',
        method: 'GET',
        data: {
          userid: userid + ''
        },
        success: function (res) {
          if (res.data.code === 0) {
            // 请求成功，返回成功
            // ...
          } else {
            // 请求成功，返回错误
            wx.showToast({
              title: '数据返回错误',
              image: '/images/toast_warning.png',
              duration: 2000
            })
          }
        },
        fail: function () {
          // 请求失败 
          wx.showToast({
            title: '请求失败',
            image: '/images/toast_warning.png',
            duration: 2000
          })
        },
        complete: function () {
          // 不管是请求成功还是失败
        }
    })
    
    },
    ```
#### Page参数内的方法声明顺序
使用微信开发者工具新建一个Page时，在`.js`的`Page`函数的参数内自带了一些属性和方法，自定义方法放在这些方法后面。

#### promise的使用
#### 使用唯一值来操作数据,用索引操作数据