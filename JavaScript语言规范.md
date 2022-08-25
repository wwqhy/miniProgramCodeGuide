 
#### 前奏
约定JavaScript使用ES6标准开发
 
wxs(WeiXin Script)和JavaScript是不同的语言，有自己的语法，wxs请参考[wxs文档](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxs/)，这里的规范仅针对js。

#### 关键字
任何时候，避免使用语言保留关键字命名。
#### 变量声明
使用`let`代替`var`声明变量，
```
let loadding = -1;
loadding = 0;
```
使用`const`声明常量，常量名要求大写，多个词之间以下划线`_`连接。
```
const { HOST, GET_URL } = require("../../utils/api.js");
```
js允许一个声明可以有多个变量。我们约定，一个声明只有一个变量。
- 推荐写法
    ```
    let a = 0; 
    let b = 1;
    let c = 2;
    ```
- 不推荐写法
    ```
    let a = 0, b = 1, c = 2;
    ```
<!--
#### 分号
语句结束，统一添加分号`;`
- 推荐写法
    ```
    let loadding = -1;
    if( loadding === 0) {
        console.log('加载完成');
        return false;
    } else {
        console.log('加载未完成');
        return true;
    }
    ```
- 不推荐写法
    ```
    let loadding = -1
    if( loadding === 0) {
        console.log('加载完成') ;
        return false
    } else {
        console.log('加载未完成')
        return true
    }
    ```
--->
<!--
已有项目中都加了分号
可以避免代码压缩时的一些坑
-->
#### 字符串
字符串统一使用单引号`''`，不使用双引号`""`
```
let title = '中国火星探测器气动设计已完成 正进行试验验证';
```
字符串需要换行或由代码生成的字符串时使用模板字符串 ``` `` ```
- 推荐写法
    ```
    // 字符串换行
    let content = `据了解，我国火星探测任务力争一次实现环绕、
      着陆和巡视三大目标。其中，着陆器的着陆过程涉及到多项空
      气动力学难题。`;
      
    // 代码拼接生成字符串
    let editor = '付毅飞';
    let text = `责任编辑${editor}`; 
    ```
- 不推荐写法
    ```
    // 字符串换行,使用 \n
    let content = '据了解，我国火星探测任务力争一次实现环绕、 \n 着陆和巡视三大目标。其中，着陆器的着陆过程涉及到多项空 \n气动力学难题。';
      
    // 代码拼接生成字符串
    let editor = '付毅飞';
    let text = '责任编辑' + editor; 
    ```
#### 函数
使用箭头函数。箭头函数不仅简洁，还可以保留`this`指向
```
[1,2,3].map((item, index) => {
  let res = item + index;
  return res + 1;
});
```
函数只有一个参数时，参数的`()`省略:
```
let show = a => {
    alert(a*2);
}
```
函数体只有一个return语句时，函数体的`{}`省略：
```
let show = (a,b) => a+b;
```
#### 数组
使用字面量创建数组
```
let arr = [];
```
使用新方法forEach，map，filter，reduce处理数组数据，代码书写更简洁
- 推荐写法
    ```
    // 取出数组里的偶数
    let arr = [1,2,3,4,5,6,7,8];
    let result = arr.filter(item=>item%2===0)
    // 输出：[2, 4, 6, 8]
    ```
- 不推荐写法
    ```
    // 取出数组里的偶数
    let arr = [1,2,3,4,5,6,7,8];
    let result = [];
    for(let i=0; i<arr.length; i++) {
      let item = arr[i];
      if(item%2===0) {
          result.push(item)
      }
    }
    // 输出：[2, 4, 6, 8]
    ```
使用解构赋值和扩展运算符`...`简化代码
#### 对象
使用字面量值创建函数
```
let obj = {};
```

属性简写，属性名跟值的变量（key和value）一样时，只写属性名
- 推荐写法
    ```
    let a = 5;
    let obj = {
      a,
      b: 12
    }
    ```
- 不推荐写法
    ```
    let a = 5;
    let obj = {
      a：a
      b: 12
    }
    ```
方法简写，不写`function`和`:`
- 推荐写法
    ```
    let obj = {
      a:13,
      show(){
        console.log(this.a);
      }
    }
    ```
- 不推荐写法
    ```
    let obj = {
    a: 13,
      show: function(){
        console.log(this.a);
      }
    }
    ```
    
#### this

用到`this`转换的地方，统一使用`that`
```
let that = this;
```