#### 展开格式
样式代码书写一般有两种形式，一种是紧缩格式
```
.home{padding-top:44rpx;border:1rpx solid #fff;}
```
一种是展开格式
```
.home {
  padding-top: 44rpx;
  border: 1rpx solid #fff;
}
```
##### 团队约定
统一使用展开格式，这跟微信开者工具自动格式化也是一致的。
#### 缩进
统一使用2个空格代替`Tab`进行代码缩进
#### 分号
每个属性声明末尾都要加上分号`;`
- 推荐写法
    ```
    .avatar {
      width: 200rpx;
      height: 200rpx;
    }
    ```
- 不推荐写法
    ```
    .avatar {
      width: 200rpx;
      height: 200rpx
    }
    ```
#### 空格
选择器与左大括号`{`中间一个空格字符
- 推荐写法
    ```
    .name {
      color: red;
    }
    ```
- 不推荐写法
    ```
    .name{
      color: red;
    }
    ```
属性冒号与属性值之间一个空格字符
- 推荐写法
    ```
    .name {
      color: red;
    }
    ```
- 不推荐写法
    ```
    .name {
      color:red;
    }
    ```
逗号分割的属性值，逗号后面一个空格字符
- 推荐写法
    ```
    .name {
      color: rgba(125, 125, 125, 1);
      box-shadow: 1px 1px 1px #333, 2px 2px 2px #ccc;
    }
    ```
- 不推荐写法
    ```
    .name {
      color: rgba(125,125,125,1);
      box-shadow: 1px 1px 1px #333,2px 2px 2px #ccc;
    }
    ```
<!-- 
并列选择器需要为每个选择器单独开户一行
- 推荐写法
```
.name,
.nick {
  color: red;
}
```
- 不推荐写法
```
.name,.nick {
  color: red;
}
```
-->
#### 属性值0
属性值为小于1的小数时，省略小数点前的0
- 推荐写法
    ```
    .name {
      color: rgba(125, 125, 125, .5);
    }
    ```
- 不推荐写法
    ```
    .name {
      color: rgba(125, 125, 125, 0.5);
    }
    ```

避免为属性值0指明单位
- 推荐写法
    ```
    .box {
      margin: 0 22rpx;
    }
    ```
- 不推荐写法
    ```
    .box {
      margin: 0rpx 22rpx;
    }
    ```
#### 十六进制
属性值为十六进制时，尽量使用简写
- 推荐写法
    ```
    .name {
      color: #fff;
    }
    ```
- 不推荐写法
    ```
    .name {
      color: #ffffff;
    }
    ```
#### 大小写
选择器，属性名，属性值统一使用小写
- 推荐写法
    ```
    .setting {
      display: flex
    }
    ```
- 不推荐写法
    ```
    .SETTING {
      DISPLAY: FLEX
    }
    .setting {
      DISPLAY: flex
    }
    ```
#### 使用双引号
统一使用双引号`""`
- 推荐写法
    ```
    @import "common.wxss";
    
    .setting {
      content: " ";
    }
    ```
- 不推荐写法
    ```
    @import 'common.wxss';
    
    .setting {
      content: ' ';
    }
    ```
#### 选择器
不使用id选择器

- 推荐写法
    ```
    .overview {
      color: blue;
    }
    ```
- 不推荐写法
    ```
    #overview {
      color: blue;
    }
    ```
不使用无具体语义的标签选择器
- 推荐写法
    ```
    .nickname text {
      color: red;
    }
    ```
- 不推荐写法
    ```
    view text{
      color: red;
    }
    ```
#### 简写的属性
应该尽量限制使用简写形式的属性声明。过渡使用过简写形式的属性声明，会对属性值产生不必要的覆盖从而引起副作用。
- 推荐写法 
    ```
    .box {
      padding-top: 44rpx;
      padding-left: 44rpx;
      background-color: red;
      background-image: url("image.jpg");
    }
    ```
- 不推荐写法
    ```
    .box {
      padding: 44rpx 0 0 44rpx;
      background: red;
      background: url("image.jpg");
    }
    ```
#### 属性书写顺序
由于布局定位属性可以从正常文档流中移除元素，并且能覆盖盒模型的相关样式，所以放在首位。盒模型决定了盒子的尺寸，大小，排在第二位。建议遵循以下顺序：
1. 布局定位属性：display / position / float / clear / visibility / overflow
2. 自身属性（盒模型）：width / height / margin / padding / border / background
3. 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
4. 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient …

示例
```
.box {
    display: block;
    position: relative;
    float: left;
    width: 100rpx;
    height: 100rpx;
    margin: 0 10rpx;
    padding: 20rpx 0;
    font-size: 36rpx;
    color: #333;
    background: rgba(0, 0, 0, .5);
    border-radius: 10px;
}
```
#### 避免重申选择器
同一选择器的样式只应出现一次，反复重申选择器样式，会造成样式代码混乱，难以维护
- 推荐写法
    ```
    .name {
      color: #fff;
      font-size: 22rpx;
    }
    ```
- 不推荐写法
    ```
    .name {
      color: #eee;
    }
    
    .name {
      color: #fff;
      font-size: 22rpx;
    }
    ```
#### 样式块间隔
样式块与样式块相隔一行
- 推荐写法
    ```
    ...
    
    .avatar {
      width: 200rpx;
      height: 200rpx;
    }
    
    .name {
      color: #fff;
    }
    
    ...
    ```
- 不推荐写法
    ```
    ...
    .avatar {
      width: 200rpx;
      height: 200rpx;
    }
    .name {
      color: #fff;
    }
    ...
    ```
#### 模块间隔
模块与模块间相隔两行
- 推荐写法
    ```
    /* 模块A
    -------------------------------------------------- */
    .modules_a {}
    
    
    /* 模块B
    -------------------------------------------------- */
    .modules_b {}
    ```
- 不推荐写法
    ```
    /* 模块A
    -------------------------------------------------- */
    .modules_a {}
    /* 模块B
    -------------------------------------------------- */
    .modules_b {}
    ```
