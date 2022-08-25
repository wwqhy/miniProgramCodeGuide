#### 前奏
约定JavaScript使用ES6标准开发
 
wxs(WeiXin Script)和JavaScript是不同的语言，有自己的语法，wxs请参考[wxs文档](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxs/)，这里的规范仅针对js。

#### 变量命名

关于变量命名，主流分为驼峰式命名和下划线式命名两大阵营。我们约定，统一使用驼峰式命名。
- 推荐写法
    ```
    let userId = 654321; 
    function getUserInfo () {
      ....
    }
    ```
- 不推荐写法
    ```
    let user_id = 654321; 
    function get_user_info () {
      ....
    }
    ```



#### 分号

尽管现在JavaScript引擎知道该在什么情况下自动添加分号，由于项目历史原因和避免代码压缩时产生不必要的问题，我们约定使用分号。分号紧跟代码的最后一个字符。
- 推荐写法
    ```
    let loading = -1;
    ```
- 不推荐写法
    ```
    let loading = -1 ;
    ```
#### 逗号

逗号分割列表时，逗号放置在当前行的末尾。

- 推荐写法
    ```
    let bar = 1, 
        foo = 2;
    ```
- 不推荐写法
    ```
    let bar = 1 
        , foo = 2;
    ```
    
数组（或对象）的最后一个元素（或属性）后面的逗号是拖尾逗号，示例：
```
 let o = {
   a: 1,
   b: 2, // 拖尾逗号
 }
```
对于数组和对象，最后一个元素或属性与右括号`]`或`}`不在同一行时，可以（但不要求）使用拖尾逗号；在同一行时，禁止使用拖尾逗号。
- 推荐写法
    ```
    let arr = ['name',
      'age',
      'gender',
    ]
    let o1 = {a: 1,b: 2};
    let o2 = {
      a: 1,
      b: 2,
    };
    ```
- 错误写法
    ```
    let arr = ['name','age','gender',]
    let o1 = {a: 1,b: 2,}
    ```
    
#### 缩进

统一使用2个空格字符进行代码缩进。

#### 空格

##### 操作符

操作符前后加一个空格字符。

- 推荐写法
    ```
    let a = 1 + 2;
    ```
- 不推荐写法
    ```
    let a = 1+2;
    ```
##### 逗号
同一行内代码用到逗号，逗号后面加一个空格字符，提高代码可读性。

- 推荐写法
    ```
    let bar = 1, foo = 2;
    let arr = [1, 2, 3, 4, 5];
    ```
- 不推荐写法
    ```
    let bar = 1,foo = 2;
    let arr = [1,2,3,4,5]
    ```
##### 函数
函数声明式声明函数时，函数名与参数括号`()`连在一起，之间不加空格；参数括号`()`与函数体的左大括号`{`之间一个空格字符。
- 推荐写法
    ```
    function getInfo(userId) {
      ...
    }
    ```
- 不推荐写法
    ```
    function getInfo1 (userId) {
      ...
    }
    
    function getInfo2(userId){
      ...
    }
    ```
函数字面量里，关键字`function`与参数括号`()`之间一个空格字符，参数括号`()`与函数体的左大括号`{`之间一个空格字符。
- 推荐写法
    ```
    let getInfo = function (userId) {
      ...
    }
    ```
- 不推荐写法
    ```
    let getInfo1 = function(userId) {
      ...
    }
    
    let getInfo2 = function(userId){
      ...
    }
    ```
函数调用时，禁止有空格。
- 推荐写法
    ```
    getInfo();
    ```
- 错误写法
    ```
    getInfo ();
    ```
##### 对象字面量
对象字面量的属性名和冒号`:`之间不能有空格字符，冒号`:`和属性值之间一个空格字符。

- 推荐写法
    ```
    let o1 = { a: 1, b: 2, c: 3 }
    let o2 = {
        e: 5,
        f: 6,
        g: 7,
    }
    ```
- 不推荐写法
    ```
    let o1 = { a:1, b :2, c : 3}
    let o2 = {
        e:5,
        f :6,
        g : 7,
    }
    ```
对象字面量在一行内时，左括号`{`和右括号`}`与代码各间隔一个空格字符。
- 推荐写法
    ```
    let o1 = { a: 1, b: 2, c: 3 }
    ```
- 不推荐写法
    ```
    let o1 = {a: 1, b: 2, c: 3}
    ```  
##### 单行代码
在单行代码中使用空格。

- 推荐写法
    ```
    function foo() { return true }
    if (true) { return true }
    ```
- 不推荐写法
    ```
    function foo(){return true}
    if(true){return true}
    ```
##### 代码块
大括号`{}`包裹起来的代码叫代码块，示例：
```
{
  let userId = 654321;
}
```
代码块前统一加一个空格字符
- 推荐写法
    ```
    if (true) {
      return '成功！' 
    }
    
    function getInfo() {
      ...
    }
    ```
- 不推荐写法
    ```
    if (true){
      return '成功！' 
    }
    
    function getInfo(){
      ...
    }
    ```
##### 计算属性
在对象的计算属性内，禁止有空格。
- 推荐写法
    ```
    obj['name']
    ```
- 不推荐写法
    ```
    obj['name' ]
    obj[ 'name']
    ```
#### 空行

空行对分离代码逻辑有帮助，但过多的空行会占据太多的屏幕空间，影响代码可读性。我们约定，最大连续空行数为2。

- 推荐写法
    ```
    if(true) {
      console.log('成功！');
    }
    
    function getUserInfo () {
      ...
    }
    ```

- 不推荐写法
    ```
    if(true) {
      console.log('成功！');
    }
    
    
    
    
    function getUserInfo () {
      ...
    }
    ```
    
在非空文件中，拖尾空行可以减少版本控制时的代码冲突。

- 推荐写法
```
function getUserInfo () {
  ...
}

// ↑上面一行是空行
```

- 不推荐写法
```
function getUserInfo () {
  ...
}
```
#### 大括号`{}`风格
用来描述大括号`{}`与代码块相对位置的方法很多，如下：
- 风格一
    ```
    if (true) {
      console.log('true');  
    } else {
      console.log('false');
    }
    ```
- 风格二
    ```
    if (true) {
      console.log('true');  
    } 
    else {
      console.log('false');
    }
    ```
- 风格三
    ```
    if (true) 
    {
      console.log('true');  
    }
    else
    {
      console.log('false');
    }
    ```
我们约定，使用风格一。
