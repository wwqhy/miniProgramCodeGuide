#### class选择器命名基本规则
- 以字母开头，全部字母小写

- 尽量简短、明确

- 单个名字如果由多个词组成，单词间以下划线`_`连接
    ```
    <view class="user_info">
    ... 
    </view>
    ```
- 层级关系以中划线`-`连接
    ```
    <view class="user_info-avatar">
    ... 
    </view>
    
    <text class="notice-title"> ... </text>
    
    ```
    
#### 继承式命名


为了保证我们设计的class样式既能重复利用，又能避免冲突。我们采用继承式来给class样式命名。

每个页面一般都可以分成几个模块，我们把每个模块最外层的class名作为祖先，模块内部的class样式名用祖先名作为前缀，它们以中划线`-`连接。（通过这种方式来表示class样式的作用域）
```
  // home是祖先模块，user和event是home的直接子模块
  <view class="home">
    <view class="home-user">
      // 用户信息
    </view> 
    <view class="home-event">
      // 动态详情
    </view> 
  </view>
```
在页面结构里，模块内部可以有子模块，子模块下面可以有孙子模块，以此类推。class样式命名也按这个层级。
```
  // home是祖先模块，user和event是home的直接子模块
  // user下面又有两个子模块name和signature
  <view class="home">
    <view class="home-user">
      <view class="home-user-name">
        // 用户信息
      </view>
      <view class="home-user-signature">
        // 个性签名
      </view> 
    </view> 
    <view class="home-event">
      // 动态详情
    </view> 
  </view>
```
#### 缩写
当页面结构复杂，层级过多，样式名的前缀就会太多太长，我们需要对前缀进行缩写。

当样式名的前缀太多(一般超过2个)或太长，我们把每两个前缀作为一组，取每个前缀的第一个字母合在一起组成新的前缀，前缀与前缀或class样式之间以中划线`-`连接。缩写时要保证新的前缀具有唯一性和可辨识性。
```
  // home是祖先模块，user和event是home的直接子模块
  // user下面又有两个子模块name和signature
  <view class="home">
    <view class="home-user">
      // hu就home-user的缩写
      <view class="hu-name">
        // 用户信息
      </view>
      <view class="hu-signature">
        // 个性签名
      </view> 
    </view> 
    <view class="photos-desc">
      // he 是photos-desc缩写
      <view class="he-photos">
        <image class="he-photos-image" src="..."></image> 
        <view class="he-photos-desc">
          // pd 是photos-desc的缩写
          <text class="he-pd-text">...</text>
        </view>
      </view> 
      <view class="he-video">
        ...
      </view> 
    </view> 
  </view>
```
<!--- 特殊化以双中划线`--` 连接-->
<!--    ```-->
<!--    <text class="notice-title notice-title--small"> ... </text>-->
<!--    ```-->
#### 常用命名推荐

ClassName|含义
---|---
about	|关于
account	|账户
arrow	|箭头图标
article	|文章
aside	|边栏
audio	|音频
avatar	|头像
bg,background	|背景
bar	|栏（工具类）
branding	|品牌化
crumb,breadcrumbs	|面包屑
btn,button	|按钮
caption	|标题，说明
category	|分类
chart	|图表
clearfix	|清除浮动
close	|关闭
col,column	|列
comment	|评论
community	|社区
container	|容器
content	|内容
copyright	|版权
current	|当前态，选中态
default	|默认
description	|描述
details	|细节
disabled	|不可用
entry	|文章，博文
error	|错误
even	|偶数，常用于多行列表或表格中
fail	|失败（提示）
feature	|专题
fewer	|收起
field	|用于表单的输入区域
figure	|图
filter	|筛选
first	|第一个，常用于列表中
footer	|页脚
forum	|论坛
gallery	|画廊
group	|模块，清除浮动
header	|页头
help	|帮助
hide	|隐藏
hightlight	|高亮
home	|主页
icon	|图标
info,information	|信息
last	|最后一个，常用于列表中
links	|链接
login	|登录
logout	|退出
logo	|标志
main	|主体
menu	|菜单
meta	|作者、更新时间等信息栏，一般位于标题之下
module	|模块
more	|更多（展开）
msg,message	|消息
nav,navigation	|导航
next	|下一页
nub	|小块
odd	|奇数，常用于多行列表或表格中
off	|鼠标离开
on	|鼠标移过
output |输出
pagination	|分页
pop,popup	|弹窗
preview	|预览
previous	|上一页
primary	|主要
progress	|进度条
promotion	|促销
rcommd,recommendations	|推荐
reg,register	|注册
save	|保存
search	|搜索
secondary	|次要
section	|区块
selected	|已选
share	|分享
show	|显示
sidebar	|边栏，侧栏
slide	|幻灯片，图片切换
sort	|排序
sub	|次级的，子级的
submit	|提交
subscribe	|订阅
subtitle	|副标题
success	|成功（提示）
summary	|摘要
tab	|标签页
table	|表格
txt,text	|文本
thumbnail	|缩略图
time	|时间
tips	|提示
title	|标题
video	|视频
wrap	|容器，包，一般用于最外层
wrapper	|容器，包，一般用于最外层