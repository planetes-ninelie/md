# 1 JavaScript

## Day 1

### 1.1.1 JavaScript书写位置

​	页面弹出警示框

```JavaScript
 <script>
    alert('你好，js~')
 </script>
```

​	

### 1.1.2  多行注释

​	单行注释 ctrl + /

​	多行注释 shift + alt + a

​	要么统一写分号，要么不写



### 1.1.3 js输入、输出和字面量

#### 	1.1.3.1 文档输出内容

```
<script>
    document.write('<div>hello</div>')
    document.write('hi')
</script>
```

#### 	1.1.3.2 输入语句

```
<script>
    prompt('请输入数字')
</script>
```

#### 	1.1.3.3 JavaScript 代码执行顺序：

按HTML文档流顺序执行JavaScript代码，alert() 和 prompt() 它们会跳过页面渲染先被执行（目前作为了解，后期讲解详细执行过程）

### 

### 1.2 变量

#### 	1.2.1 变量的使用

```
 <script>
    let age = 18
  </script>
```

#### 	1.2.2 变量名的命名规则

​		关于变量的名称（标识符）有一系列的规则需要遵守：

​		1.只能是字母、数字、下划线、$，且不能能数字开头

​		2.字母区分大小写，如 Age 和 age 是不同的变量

​		3. JavaScript 内部已占用于单词（关键字或保留字）不允许使用

​		4.尽量保证变量具有一定的语义，见字知义

​		注：所谓关键字是指 JavaScript 内部使用的词语，如 `let` 和`var`，保留字是指 JavaScript 内部目前没有使用的词语，但是将来可能会使用词语。

#### 	1.2.3 关键字

​		JavaScript 使用专门的关键字 `let` 和 `var` 来声明（定义）变量，在使用时需要注意一些细节：

​			以下是使用 `let` 时的注意事项：

- 允许声明和赋值同时进行
- 不允许重复声明
- 允许同时声明多个变量并赋值
- JavaScript 中内置的一些关键字不能被当做变量名

​			以下是使用 `var` 时的注意事项：

- 允许声明和赋值同时进行
- 允许重复声明
- 允许同时声明多个变量并赋值

​		大部分情况使用 `let` 和 `var` 区别不大，但是 `let` 相较 `var` 更严谨，因此推荐使用 `let`，后期会更进一步介绍二者间的区别。



### 1.3 常量

概念：使用 const 声明的变量称为“常量”。

使用场景：当某个变量永远不会改变的时候，就可以使用 const 来声明，而不是let。

命名规范：和变量一致

~~~javascript
const PI = 3.14
~~~

>注意： 常量不允许重新赋值,声明的时候必须赋值（初始化）



### 1.4 数据类型

#### 1.4.1 数值类型

```
 <script> 
    let score = 100 // 正整数
    let price = 12.345 // 小数
    let temperature = -40 // 负数

    document.write(typeof score) // 结果为 number
    document.write(typeof price) // 结果为 number
    document.write(typeof temperature) // 结果为 number
  </script>
```

#### 1.4.2 模板字符串

```
  <script>
    let name = prompt('name')
    let age = prompt('age')
    document.write(`大家好，我叫${name},今年${age}岁了`)
  </script>
```

#### 1.4.3 null和undefined区别：

​	undefined表示没有赋值

​	null表示赋值了，但是内容为空

```
<script>
    console.log(undefined + 1) // NaN
    console.log(null + 1) // 1
  </script>
```

#### 1.4.4 隐式转换

某些运算符被执行时，系统内部自动将数据类型进行转换，这种转换称为隐式转换。

规则： 1.+ 号两边只要有一个是字符串，都会把另外一个转成字符串 

​			2.除了+以外的算术运算符 比如 - * / 等都会把数据转成数字类

缺点： 转换类型不明确，靠经验才能总结 

小技巧：1.+号作为正号解析可以转换成数字型 

```
<script>
    console.log(+'123')
  </script>
```

​			2.任何数据和字符串相加结果都是字符串

#### 1.4.5 显示转换

```
 <script>
 	console.log(NUmber('12.34')) //转化为数字
    console.log(parseInt('12.34px')) //保留整数
    console.log(parseFloat('12.34px')) //保留小数
  </script>
```



## Day 2

### 2.1 运算符

#### 2.1.1 前置自增和后置自增

```
 <script>
    let i = 1
    console.log(++i + 2) //4
    console.log(i++ + 2) //3
  </script>
```

#### 2.1.2 逻辑运算符

| 符号 | 名称   | 日常读法 | 特点                       | 口诀           |
| ---- | ------ | -------- | -------------------------- | -------------- |
| &&   | 逻辑与 | 并且     | 符号两边有一个假的结果为假 | 一假则假       |
| \|\| | 逻辑或 | 或者     | 符号两边有一个真的结果为真 | 一真则真       |
| !    | 逻辑非 | 取反     | true变false  false变true   | 真变假，假变真 |



## Day 3

### 3.1 操作数组

数组做为对象数据类型，不但有 `length` 属性可以使用，还提供了许多方法：

1. push 动态向数组的尾部添加一个单元
2. unshit 动态向数组头部添加一个单元
3. pop 删除最后一个单元
4. shift 删除第一个单元
5. splice 动态删除任意单元

使用以上4个方法时，都是直接在原数组上进行操作，即成功调任何一个方法，原数组都跟着发生相应的改变。并且在添加或删除单元时 `length` 并不会发生错乱。

```
<script>
  // 定义一个数组
  let arr = ['html', 'css', 'javascript']

  // 1. push 动态向数组的尾部添加一个单元
  arr.push('Nodejs')
  console.log(arr)
  arr.push('Vue')

  // 2. unshit 动态向数组头部添加一个单元
  arr.unshift('VS Code')
  console.log(arr)

  // 3. splice 动态删除任意单元
  arr.splice(2, 1) // 从索引值为2的位置开始删除1个单元
  console.log(arr)

  // 4. pop 删除最后一个单元
  arr.pop()
  console.log(arr)

  // 5. shift 删除第一个单元
  arr.shift()
  console.log(arr)
</script>
```



## Day 4

### 4.1 函数

1.函数名相同的，后面覆盖前面

### 4.2 作用域

```
<script>
    let num = 10  // 1. 全局变量
    console.log(num)
    function fn() {
      console.log(num)
    }
    fn()

    // 2. 局部变量
    function fun() {
      let str = 'pink'
    }
    console.log(str)  // 错误
  </script>
```

### 4.3 匿名函数

```
(function(){ xxx  })();
(function(){xxxx}());
```



### 4.4 逻辑中断

```

  <script>
    function fn(x, y) {
      x = x || 0
      y = y || 0
      console.log(x + y)
    }
    fn(1, 2)
    // fn()

    // console.log(false && 22)
    // console.log(false && 3 + 5)
    // let age = 18
    // console.log(false && age++) // age++ 不执行  一假则假
    // console.log(age)

    // console.log(true || age++)
    // console.log(age)


    // console.log(11 && 22)  // 都是真，这返回最后一个真值
    // console.log(11 || 22)  //  输出第一个真值
  </script>
```

### 4.5 布尔型

tips: ’ ‘ 、0、undefined、null、false、NaN转换为布尔值后都是false，其余为true



## Day5 

### 5.1 对象

#### 5.1.1  对象的引用

```
 let obj = {
      'goods-name': '小米10青春版',
      num: '100012816024',
      weight: '0.55kg',
      address: '中国大陆'
    }
   
    // console.log(obj.goods - name)
    // 查的另外一种属性：
    // 对象名['属性名']
    console.log(obj['goods-name'])
```

#### 5.1.2 对象的方法

```
  <script>
    let obj = {
      uname: 'Chelly',
      song: function(x) {
        console.log('planetes',x)
      }
    }
    obj.song('i')
  </script>
```

#### 5.1.3 Math

`Math` 是 JavaScript 中内置的对象，称为数学对象，这个对象下即包含了属性，也包含了许多的方法。

属性

- Math.PI，获取圆周率

```javascript
// 圆周率
console.log(Math.PI);
```

方法

- Math.random，生成 0 到 1 间的随机数

```javascript
// 0 ~ 1 之间的随机数, 包含 0 不包含 1
Math.random()
//0 ~ 10 之间的数
Math.random() * 10 + 1
//N - M 之间的数
Math.floor(Math.random() * (M - N + 1)) + N
```

- Math.ceil，数字向上取整

```javascript
// 舍弃小数部分，整数部分加1
Math.ceil(3.4)
```

- Math.floor，数字向下取整

```javascript
// 舍弃小数部分，整数部分不变
Math.floor(4.68)
```

- Math.round，四舍五入取整

```javascript
// 取整，四舍五入原则
Math.round(5.46539)
Math.round(4.849)
```

- Math.max，在一组数中找出最大的

```javascript
// 找出最大值
Math.max(10, 21, 7, 24, 13)
```

- Math.min，在一组数中找出最小的

```javascript
// 找出最小值
Math.min(24, 18, 6, 19, 21)
```

- Math.pow，幂方法

```javascript
// 求某个数的多少次方
Math.pow(4, 2) // 求 4 的 2 次方
Math.pow(2, 3) // 求 2 的 3 次方
```

- Math.sqrt，平方根

```javascript
// 求某数的平方根
Math.sqrt(16)
```

数学对象提供了比较多的方法，这里不要求强记，通过演示数学对象的使用，加深对对象的理解。





# 2 webAPIs

## Day 1

### 1.1 变量声明const优先

变量声明有三个 var let 和 const l 我们应该用那个呢？ 

首先var 先排除，老派写法，问题很多，可以淘汰掉… 

let or const ? 

建议： const 优先，尽量使用const，原因是： 

​	Ø const 语义化更好 

​	Ø 很多变量我们声明的时候就知道他不会被更改了，那为什么不用 const呢？

​	Ø 实际开发中也是，比如react框架，基本const

 l如果你还在纠结，那么我建议：有了变量先给const，如果发现它后面是要被修改的，再改为let

const 声明的值不能更改，而且const声明变量的时候需要里面进行初始化 l 但是对于引用数据类型，const声明的变量，里面存的不是 值，不是值，不是值，是 地址

### 1.2 获取DOM元素

1.根据CSS选择器来获取DOM元素

```
document.querySelector('.nav li')	//选择匹配的第一个元素

document.querySelectorAll('.nav li')	//选择匹配的多个元素

/* 
只能通过遍历的方式一次给里面的元素做修改
得到的是一个伪数组
有长度有索引号的数组
但是没有 pop() push() 等数组方法
想要得到里面的每一个对象，则需要遍历（for）的方式获得
*/
const lis = document.querySelectorAll('.nav li')
for (let i = 0; i < lis.length; i++) {
  console.log(lis[i])
}

```

### 1.3 其他获取DOM元素

```
//根据id获取一个元素
document.getElementById('nav')
//根据标签获取一类元素
document.getElementsByTagName('div')
//根据类名获取元素
document.getElementsByClassName('w')
```

### 1.4 操作元素内容

```
//innerHTML
const tag = document.querySelector('.name')
tag.innerHTML = ‘name’

//innerText
const tag = document.querySelector('.name')
tag.innerText = ‘name’
```

### 1.5 操作元素属性

```
1.操作元素常用属性
	//最常见的属性比如： href、title、src
	const pic = document.querySelector('img')
	pic.src='./images/b02.jpgpic.title ='刘德华黑马演唱会'


2.操作元素样式属性
	//通过 style 属性操作CSS
	const box = document.querySelector('.box')
    box.style.width='200px'
    box.style.marginTop ='15px'
    box.style.backgroundcolor ='pink'
    
	//操作类名(className) 操作CSS
	//className是使用新值换旧值, 如果需要添加一个类,需要保留之前的类名
	const div = document.querySelector('div')
    div.className = 'type2'
    
	//通过 classList 操作类控制CSS
	const div = document.querySelector('div')
    div.classList.add('type2')
    div.classList.remove('type2')
    div.classList.toggle('type2')
    
 
 3.操作表单元素样式
 	const uname = document.querySelector('input')
    uname.type = 'password'
    
    //常见的：disabled、checked、selected
    const ipt = document.querySelector('input')
    // ipt.checked = 'true' //会选择，隐式转换，不提倡
    ipt.checked = true
    
  
  4.自定义属性
  <div data-id="1"></div>
  <script>
    const one = document.querySelector('div')
    console.log(one.dataset)
  </script>
```

### 1.6 间歇函数

```
1.开启定时器
<script>
    setInterval(function(){
      console.log('一秒执行一次')
    },1000)

    // setInterval(函数名,间隔时间)
    function fn() {
      console.log('一秒执行一次')
    }
    setInterval(fn,1000)
    setInterval('fn()',1000)
</script>

2.关闭定时器
<script>
 	let n = setInterval(fn,1000)
    clearInterval(n)
</script>
```



## Day2

### 2.1 事件监听和类型

#### 2.1.1 点击事件

DOM L0 事件源.on事件 = function() { } 

DOM L2 事件源.addEventListener(事件， 事件处理函数)

区别： on方式会被覆盖，addEventListener方式可绑定多次，拥有事件更多特性，推荐使用

```
<script>
    const btn = document.querySelector('.event')
    btn.addEventListener('click',function() {
      alert('hello')
    })
</script>

```

#### 2.1.2 鼠标移动事件

```
<body>
  <div>好</div>
  <script>
    const div = document.querySelector('div')
    div.addEventListener('mouseenter',function() {
      console.log(`来了！`)
    })
    div.addEventListener('mouseleave',function() {
      console.log(`走了！`)
    })
  </script>
</body>
```

#### 2.1.3 焦点事件

```
<body>
  <input type="text">
  <script>
    const input = document.querySelector('input')
    input.addEventListener('focus',function() {
      console.log('焦点触发')
    })
    input.addEventListener('blur',function() {
      console.log('失去焦点触发')
    })
  </script>
</body>
```

#### 2.1.4 键盘事件

```
<body>
  <input type="text">
  <script>
    const input = document.querySelector('input')
    input.addEventListener('keydown', function () {
      console.log('键盘按下了')
    })
    input.addEventListener('keyup', function () {
      console.log('键盘弹起了')
    })
  </script>
</body>
```

#### 2.1.5 输入事件

```
<body>
  <input type="text">
  <script>
    const input = document.querySelector('input')
    input.addEventListener('input', function () {
      console.log(input.value)
    })
  </script>
</body>
```

补充：'change' 输入的值改变时进行事件

### 2.2 事件对象

```
<input type="text"></input>
<script>
const btn = document.querySelector('input')
btn.addEventListener('keyup', function(e) {
  if (e.key === 'Enter') {
    console.log('按下了回车键')
  }
})
</script>
```

tips：消除str里首尾空格的方法trim()



### 2.3 环境对象

目标：能够分析判断函数运行在不同环境中 this 所指代的对象 

环境对象：指的是函数内部特殊的变量 this ，它代表着当前函数运行时所处的环境 

作用：弄清楚this的指向，可以让我们代码更简洁 

 	函数的调用方式不同，this 指代的对象也不同 

​	【谁调用， this 就是谁】 是判断 this 指向的粗略规则

​	直接调用函数，其实相当于是 window.函数，所以 this 指代

### 

### 2.4 回调函数

如果将函数 A 做为参数传递给函数 B 时，我们称函数 A 为回调函数 

简单理解： 当一个函数当做参数来传递给另外一个函数的时候，这个函数就是回调函数

```
<script>
function fn() {
  console.log('回调函数');
}
setInterval(fn, 1500)
</script>
```



## Day3

### 3.1 全选反选实现代码

```
<!DOCTYPE html>

<html>

<head lang="en">
  <meta charset="UTF-8">
  <title></title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    table {
      border-collapse: collapse;
      border-spacing: 0;
      border: 1px solid #c0c0c0;
      width: 500px;
      margin: 100px auto;
      text-align: center;
    }

    th {
      background-color: #09c;
      font: bold 16px "微软雅黑";
      color: #fff;
      height: 24px;
    }

    td {
      border: 1px solid #d0d0d0;
      color: #404060;
      padding: 10px;
    }

    .allCheck {
      width: 80px;
    }
  </style>
</head>

<body>
  <table>
    <tr>
      <th class="allCheck">
        <input type="checkbox" name="" id="checkAll"> <span class="all">全选</span>
      </th>
      <th>商品</th>
      <th>商家</th>
      <th>价格</th>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米手机</td>
      <td>小米</td>
      <td>￥1999</td>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米净水器</td>
      <td>小米</td>
      <td>￥4999</td>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米电视</td>
      <td>小米</td>
      <td>￥5999</td>
    </tr>
  </table>
  <script>
    const checkAll = document.querySelector('#checkAll')
    const cks = document.querySelectorAll('.ck')
    checkAll.addEventListener('click', function () {
      // console.log(this.checked);
      for(let i = 0; i < cks.length; i++) {
        cks[i].checked = this.checked
      }
    })

    for(let i = 0; i < cks.length; i++) {
      cks[i].addEventListener('click', function () {
        checkAll.checked = document.querySelectorAll('.ck:checked').length === cks.length 
      })
    }
  </script>
</body>
</html>
```

### 3.2 事件流

#### 3.2.1 事件捕获

```
<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    // 山东  济南  蓝翔   目标（pink老师）  捕获阶段
    //  蓝翔  济南   山东   冒泡阶段
    document.addEventListener('click', function () {
      alert('我是爷爷')
    }, true)
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    }, true)
    son.addEventListener('click', function () {
      alert('我是儿子')
    }, true)
  </script>
</body>
```

#### 3.2.2 事件冒泡的阻止

```
<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    // 山东  济南  蓝翔   目标（pink老师）  捕获阶段
    //  蓝翔  济南   山东   冒泡阶段
    document.addEventListener('click', function () {
      alert('我是爷爷')
    })
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    })
    son.addEventListener('click', function (e) {
      alert('我是儿子')
      // 组织流动传播  事件对象.stopPropagation()
      e.stopPropagation()
    })
  </script>
</body>
```

#### 3.2.3 事件解绑

```
<body>
  <button>点击</button>
  <script>
    const btn = document.querySelector('button')
    // btn.onclick = function () {
    //   alert('点击了')
    //   // L0 事件移除解绑
    //   btn.onclick = null
    // }
    function fn() {
      alert('点击了')
    }
    btn.addEventListener('click', fn)
    // L2 事件移除解绑
    btn.removeEventListener('click', fn)
  </script>
</body>
```

#### 3.3.4 鼠标经过事件的冒泡

​	mouseover 和 mouseout 会有冒泡效果

​	mouseenter 和 mouseleave 没有冒泡效果

### 3.3 事件委托的案例

```
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    ul.addEventListener('click', function (e) {
      if (r.target.tagName === 'LI') {
        e.target.style.color = 'blue'
      }
    })
  </script>
</body>
```

### 3.4 阻止元素默认行为

```
<body>
  <form action="http://www.itcast.cn">
    <input type="submit" value="免费注册">
  </form>
  <a href="http://www.baidu.com">百度一下</a>
  <script>
    const form = document.querySelector('form')
    form.addEventListener('submit', function (e) {
      // 阻止默认行为  提交
      e.preventDefault()
    })

    const a = document.querySelector('a')
    a.addEventListener('click', function (e) {
      e.preventDefault()
    })
  </script>
</body>
```

### 3.5 其他事件

#### 3.5.1 页面加载事件

1.load事件 

​	监听整个页面资源给window加

2.DOMContentLoaded

​	给document加

​	无需等待样式表、图片等完全加载

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script>
    // 等待页面所有资源加载完毕，就回去执行回调函数
    // window.addEventListener('load', function () {
    //   const btn = document.querySelector('button')
    //   btn.addEventListener('click', function () {
    //     alert(11)
    //   })
    // })

    // img.addEventListener('load', function () {
    //   // 等待图片加载完毕，再去执行里面的代码
    // })

    document.addEventListener('DOMContentLoaded', function () {
      const btn = document.querySelector('button')
      btn.addEventListener('click', function () {
        alert(11)
      })
    })
  </script>
</head>
<body>
  <button>点击</button>
</body>
</html>
```

#### 3.5.2 页面滚动事件

```
<body>
  <div>
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字

  </div>
  <script>
    const div = document.querySelector('div')
    // 页面滚动事件
    window.addEventListener('scroll', function () {
      // console.log('我滚了')
      // 我想知道页面到底滚动了多少像素， 被卷去了多少  scrollTop
      // 获取html元素写法  
      // document.documentElement  
      // console.log(document.documentElement.scrollTop)
      const n = document.documentElement.scrollTop
      if (n >= 100) {
        div.style.display = 'block'
      } else {
        div.style.display = 'none'
      }
    })
    // const div = document.querySelector('div')
    // div.addEventListener('scroll', function () {
    //   // console.log(111)
    //   // scrollTop 被卷去的头部
    //   console.log(div.scrollTop)
    // })
  </script>
</body>
```

#### 3.5.3 页面尺寸事件

​	获取元素的可见部分宽高（不包含边框，margin，滚动条等） 

​	clientWidth和clientHeigh

### 3.6 元素尺寸于位置

获取宽高： 

Ø 获取元素的自身宽高、包含元素自身设置的宽高、padding、border 

Ø offsetWidth和offsetHeight 

Ø 获取出来的是数值,方便计算 

Ø 注意: 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0

获取位置： 

Ø 获取元素距离自己定位父级元素的左、上距离 

Ø offsetLeft和offsetTop 注意是只读属性

示例：

```
<body>
    <div class="header">我是顶部导航栏</div>
    <div class="content">
        <div class="sk">秒杀模块</div>
    </div>
    <div class="backtop">
        <img src="./images/close2.png" alt="">
        <a href="javascript:;"></a>
    </div>
    <script>
        const header = document.querySelector('.header')
        const sk = document.querySelector('.sk')
        window.addEventListener('scroll', function () {
            const n = document.documentElement.scrollTop
            header.style.top = n >= sk.offsetTop ? 0 : '-80px'
        })
    </script>
</body>
```

## Day4

### 4.1 日期对象

#### 4.1.1 实例化和时期对象的使用

```
<body>
  <div></div>
  <script>
    // const date = new Date()
    // console.log(date);
    // const date1 = new Date('2022-5-1 08:30:00')
    // console.log(date1);

    // console.log(date.getFullYear());
    // console.log(date.getMonth() + 1);
    // console.log(date.getDate());
    // console.log(date.getDay());
    
    //案例
    function format(i) {
      return i < 10 ? '0' + i : i
    }
    const div = document.querySelector('div')
    //div.innerHTML = time()
    setInterval(function () {
      const now = new Date()
      let year = now.getFullYear()
      let formatMon = format(now.getMonth() + 1)
      let formatDate = format(now.getDate())
      let formatHour = format(now.getHours())
      let formatMin = format(now.getMinutes())
      let seconds = format(now.getSeconds())
      
      div.innerHTML = time()
      
      function time() {
        return `${year}-${formatMon}-${formatDate}&nbsp;${formatHour}:${formatMin}:${seconds}`
      }
    }, 1000)
   

    //另外的方式
    // const div = document.querySelector('div')
    // const date = new Date()
    // div.innerHTML = date.toLocaleString() //2024/2/26 16:24:11
    // div.innerHTML = date.toLocaleDateString() //2024/2/26
    //div.innerHTML = date.toLocaleTimeString() //16:26:24
  </script>
</body>
```

#### 4.1.2 时间戳

```
<script>
    const date = new Date()
    // 三种方式获取时间戳
    console.log(date.getTime())
    console.log(+new Date())
    console.log(Date.now());

    //获取指定日期的时间戳
    console.log(+new Date('2022-4-1 18:30:00'));

    //根据日期Day() 返回星期
    const arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
    console.log(arr[new Date().getDay()]);
</script>
```

### 4.2 节点操作

#### 4.2.1 查找节点

父节点查找：子元素.parentNode

子节点查找：父元素.children

兄弟关系查找：

​	下一个兄弟节点：nextElementSibling 属性

​	上一个兄弟节点：previousElementSibling 属性

#### 4.2.2 增加节点

```
<body>
  <ul>
    <li>1</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    // 创建节点
    const li = document.createElement('li')
    //追加，插入到父元素最后一个子元素里
    li.innerHTML = '老大'
    ul.appendChild(li)

    //插入到父元素中某个子元素的前面
    const li1 = document.createElement('li')
    li1.innerHTML = '小的'
    ul.insertBefore(li1,ul.children[0])
  </script>
</body>
```

#### 4.2.3 克隆节点

```
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    const li1 = ul.children[0].cloneNode(true) //true为深克隆，false为浅克隆
    ul.appendChild(li1)
  </script>
</body>
```

#### 4.2.4 删除节点

```
  <ul>
    <li>没用了</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    ul.removeChild(ul.children[0])
  </script>
```

### 4.3 M端事件

```
  <div></div>
  <script>
    const div = document.querySelector('div')
    div.addEventListener('touchstart', function () {
      console.log('开始触摸');
    })
    div.addEventListener('touchend', function () {
      console.log('离开了');
    })
    div.addEventListener('touchmove', function () {
      console.log('一直摸');
    })
  </script>
```

### 4.4 JS插件



## Day5

### 5.1 window对象

#### 5.1.1 延时函数

```
  <script>
    setTimeout(function () {
      console.log('时间到了')
    }, 2000)
  </script>
```

#### 5.1.2 JS执行机制

JavaScript 语言的一大特点就是**单线程**，也就是说，同一个时间只能做一件事。 

这是因为 Javascript 这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作 DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之 后再删除。

 单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是： 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，**允许 JavaScript 脚本创建多个 线程**。于是，JS 中出现了同步和异步。

**同步** 

前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同 步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。 

同步任务都在主线程上执行，形成一个**执行栈**。

**异步** 

你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事 情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。 他们的本质区别： 这条流水线上各个流程的执行顺序不同

异步任务相关添加到**任务队列**中（任务队列也称为消息队列）。

**执行机制**

1. 先执行执行栈中的同步任务。 

2. 异步任务放入任务队列中。
3.  一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待 状态，进入执行栈，开始执行。

**由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为事件循环（ event loop）**

#### **5.1.3 location对象**

1.location.href

```
const url = 'https://www.bilibili.com/'
const div = document.querySelector('div')
button.addEventListener('click', function () {
  location.href = url
})
```

2.location.search

 属性获取地址中携带的参数，符号 ？后面部分

3.location.hash

hash 属性获取地址中的哈希值，符号 # 后面部

4.reload

```
const reload = document.querySelector('.reload')
reload.addEventListener('click', function () {
  location.reload(true)
})
   
//传入参数true时表示强制刷新
```

#### 5.1.4 navigator对象

通过 userAgent 检测浏览器的版本及平台

```
<script>
    // 检测 userAgent（浏览器信息）
    !(function () {
      const userAgent = navigator.userAgent
      // 验证是否为Android或iPhone
      const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
      const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
      // 如果是Android或iPhone，则跳转至移动站点
      if (android || iphone) {
        location.href = 'http://m.itcast.cn'
      }
    })();
    // !(function () { })();
    !function () { }()
</script>
```

​	tips：(function () {})() 

​			!function(){}()

​			+function(){}()

#### 5.1.5 history

```
<body>
  <button>back</button>
  <button>next</button>
  <script>
    const back = document.querySelector('button:first-child')
    const forward = back.nextElementSibling
    back.addEventListener('click', function () {
      // history.back()
      history.go(-1)
    })
    forward.addEventListener('click', function () {
      history.forward()
    })
  </script>
</body>
```

### 5.2 本地存储

#### 5.2.1 localStorage

```
  <script>
    //储存键值
    localStorage.setItem('uname', 'pink')
    //改
    localStorage.setItem('uname', 'red')
    //获取方式
    console.log(localStorage.getItem('uname'));
    //删除本地储存
    localStorage.removeItem('uname')
  </script>
```

tips：本地储存只能储存字符串数据类型，例如存入18数字最后会自动转化为‘18’

#### 5.2.2 sessionStorage

特性： 

Ø 生命周期为关闭浏览器窗口 

Ø 在同一个窗口(页面)下数据可以共享 

Ø 以键值对的形式存储使用 

Ø 用法跟localStorage 基本相同

#### 5.2.3 JSON.stringify()和JSON.parse()

```
<body>
  <script>
    const obj = {
      uname: 'cq',
      age: 21,
      gender: '女'
    }
    localStorage.setItem('obj', obj)
    //存储时无法直接获取
    console.log(localStorage.getItem('obj'));
    //所以需要转化 JSON.stringify(复杂数据类型)
    localStorage.setItem('obj',JSON.stringify(obj))
    console.log(localStorage.getItem('obj'));

    //把json字符串转化为对象
    console.log(JSON.parse(localStorage.getItem('obj')));
  </script>
</body>
```

#### 5.2.4 map()和join()

1.map()

```
const arr1 = ['Yoimiya', 'Kokomi', 'Kirara']
const arr2 = arr1.map(function (ele, index) {
  return '英文名' + ele
})
console.log(arr2);
```

2.join()

```
const arr1 = ['Yoimiya', 'Kokomi', 'Kirara']
console.log(arr1.join('|')) 
```



## Day6

### 6.1 正则表达式

#### 6.1.1 基本用法 test()方法

```
  <script>
    const str = '前端学习'
    const reg = /前端/
    console.log(!reg.test(str));
  </script>
```

#### 6.1.2 exec() 方法 

在一个指定字符串中执行一个搜索匹配，

如果匹配成功，exec() 方法返回一个数组，否则返回null

```
  <script>
    const str = '前端学习'
    const reg = /前端/
    console.log(reg.exec(str));
  </script>
```

tips：正则表达式检测查找 test方法和exec方法有什么区别？ 

Ø test方法 用于判断是否有符合规则的字符串，返回的是 布尔值 找到返回true，否则false

 Ø exec方法用于检索（查找）符合规则的字符串，找到返 回数组，否则为 nul

#### 6.1.3 元字符(特殊字符）

是一些具有特殊含义的字符，可以极大提高了灵活性和强大的匹配功能。 

Ø 比如，规定用户只能输入英文26个英文字母，普通字符的话 abcdefghijklm….. 

Ø 但是换成元字符写法：[a-z]

1.边界符（表示位置，开头和结尾，必须用什么开头，用什么结尾）

​	**^ 表示匹配行首的文本（以谁开始）**

​	**$ 表示匹配行尾的文本（以谁结束）**

2.量词（表示重复次数）

 * ***重复零次或更多次**

 * **+重复一次或更多次**

 * **？重复零次或一次**

 * **{n}重复n次**

 * **{n,}重复n次或更多次**

 * **{n,m}重复n到m次**

   tips：逗号左右两侧**千万不要出现空格**



```
  <script>
    console.log(/二哈/.test('二二哈哈')); //true

    console.log(/^二哈/.test('很二哈哈')); //false
    console.log(/^二哈/.test('二哈哈')); //true 

    console.log(/^二哈$/.test('二二哈哈')); // false
    console.log(/^二哈$/.test('一二哈三')); // false
    console.log(/^二哈$/.test('二哈')); // true
    console.log('------------------')
    //  量词 * 类似 >=0 次
    console.log(/^哈$/.test('哈')) // true
    console.log(/^哈*$/.test('')) // true
    console.log(/^哈*$/.test('哈')) // true
    console.log(/^哈*$/.test('哈哈')) // true
    console.log(/^哈*$/.test('二哈很傻')) //  false
    console.log(/^哈*$/.test('哈很傻')) //  false
    console.log(/^哈*$/.test('哈很哈')) // false
    console.log('------------------')
    //  量词 + 类似 >=1 次
    console.log(/^哈$/.test('哈')) // true
    console.log(/^哈+$/.test('')) // false
    console.log(/^哈+$/.test('哈')) // true
    console.log(/^哈+$/.test('哈哈')) // true
    console.log(/^哈+$/.test('二哈很傻')) //  false
    console.log(/^哈+$/.test('哈很傻')) //  false
    console.log(/^哈+$/.test('哈很哈')) // false
    console.log('------------------')
    console.log('------------------')
    //  量词 ? 类似  0 || 1
    console.log(/^哈?$/.test('')) // true
    console.log(/^哈?$/.test('哈')) // true
    console.log(/^哈?$/.test('哈哈')) // true
    console.log(/^哈?$/.test('二哈很傻')) //  false
    console.log(/^哈?$/.test('哈很傻')) //  false
    console.log(/^哈?$/.test('哈很哈')) // false
    // 量词 {n} 写几，就必须出现几次
    console.log(/^哈{4}$/.test('哈'))
    console.log(/^哈{4}$/.test('哈哈'))
    console.log(/^哈{4}$/.test('哈哈哈'))
    console.log(/^哈{4}$/.test('哈哈哈哈'))
    console.log(/^哈{4}$/.test('哈哈哈哈哈'))
    console.log(/^哈{4}$/.test('哈哈哈哈哈哈'))
    console.log('------------------')
    // 量词 {n,}   >=n
    console.log(/^哈{4,}$/.test('哈'))
    console.log(/^哈{4,}$/.test('哈哈'))
    console.log(/^哈{4,}$/.test('哈哈哈'))
    console.log(/^哈{4,}$/.test('哈哈哈哈'))
    console.log(/^哈{4,}$/.test('哈哈哈哈哈'))
    console.log(/^哈{4,}$/.test('哈哈哈哈哈哈'))
    console.log('------------------')
    // 量词 {n,m}  逗号左右两侧千万不能有空格    >=n && <= m
    console.log(/^哈{4,6}$/.test('哈'))
    console.log(/^哈{4,6}$/.test('哈哈'))
    console.log(/^哈{4,6}$/.test('哈哈哈'))
    console.log(/^哈{4,6}$/.test('哈哈哈哈'))
    console.log(/^哈{4,6}$/.test('哈哈哈哈哈'))
    console.log(/^哈{4,6}$/.test('哈哈哈哈哈哈'))
    console.log(/^哈{4,6}$/.test('哈哈哈哈哈哈哈'))
    console.log('------------------')
    // 字符类   [abc]  只选1个
    console.log(/^[abc]$/.test('a'))  // true
    console.log(/^[abc]$/.test('b'))  // true
    console.log(/^[abc]$/.test('c'))  // true
    console.log(/^[abc]$/.test('ab'))  // false
    console.log(/^[abc]{2}$/.test('ab'))  // true
    console.log('------------------')
    // 字符类   [a-z]  只选1个
    console.log(/^[A-Z]$/.test('p'))  // false
    console.log(/^[A-Z]$/.test('P'))  // true
    console.log(/^[0-9]$/.test(2))  // true
    console.log(/^[a-zA-Z0-9]$/.test(2))  // true
    console.log(/^[a-zA-Z0-9]$/.test('p'))  // true
    console.log(/^[a-zA-Z0-9]$/.test('P'))  // true
    console.log('------------------')
  </script>
```

3.字符类

比如：

 Ø [a-z] 表示 a 到 z 26个英文字母都可以

 Ø [a-zA-Z] 表示大小写都可以 

Ø [0-9] 表示 0~9 的数字都可

**tip：[ ] 里面加上 ^ 取反符**

预定义：

* 匹配0-9之间的任一数字，相当于[0-9]
* 匹配所有0-9以外的字符，相当于[ ^0-9]
* 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9]
* 除所有字母、数字和下划线以外的字符，相当于[^A-Za-z0-9]
* 匹配空格(包括换行符、制表符、空格符等)，相等于[\t\r\n\v\f]
* 匹配非空格的字符，相当于[ ^ \t\r\n\v\f]

#### 6.1.4 修饰符

修饰符约束正则执行的某些细节行为，如是否区分大小写、是否支持多行匹配等

i 是单词 ignore 的缩写，正则匹配时字母不区分大小写 

g 是单词 global 的缩写，匹配所有满足正则表达式的结果

```
console.log(/^java$/.test('JAVA')); //false
console.log(/^java$/i.test('JAVA')); //true
```

replace( )方法

```
console.log(str.replace(/java/i, 'JAVA')); //只能替换一个 
//JAVA和JavaScript都是编程语言
console.log(str.replace(/java/ig, 'JAVA')); //全局替换
//JAVA和JAVAScript都是编程语言
```







# 3 js进阶

## Day1

### 1.1 作用域

#### 1.1.1 局部作用域

1.块级作用域

* let和const声明的变量会产生块作用域，var不会产生块作用域
* 不同代码块之间的变量无法互相访问
* 推荐使用let或const

#### 1.1.2 全局作用域

* 不推荐为window对象动态添加属性，其默认为全局的
* 函数中未使用任何关键字声明的变量为全局变量，不推荐
* 尽可能减少声明全局变量，防止全局变量被污染

#### 1.1.3 作用域链

* 本质是底层的变量查找机制
* 函数被执行时，会优先查找当前函数作用域中查找变量1
* 如果当前作用域查不到则会优先依次逐级查找父级作用域直到全局作用

#### 1.1.4 垃圾回收机制

内存的生命周期

* 内存分配
* 内存使用
* 内存回收

tips：全局变量一般不会回收，一般情况局部变量的值不用了就会被自动回收掉

内存泄漏：程序中分配的内存由于某种原因程序未释放或无法释放叫做内存泄漏

#### 1.1.5 垃圾回收机制算法说明(GC)

* 引用计数法

​	存在问题：嵌套引用（循环引用），导致内存泄漏

* 标记清除法

​	根部已经访问不到，所以自动清除

#### 1.1.6 闭包

概念：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域

简单理解：闭包 = 内层函数 + 外层函数的变量

作用：封闭数据，实现数据私有，外部也可以访问函数内部的变量

​	闭包很有用，因为它允许将函数与其所操作的某些数据关联起来

引起的问题：内存泄漏

#### 1.1.7 变量提升

概念：它允许在变量声明之前被访问（仅存在var声明变量）

tips：

* 变量在未声明之前即被访问，变量值为undefined
* 变量在未声明即被访问时会报语法错误
* let/const声明的变量不存在变量提升
* 变量提升出现在相同作用域当中
* 实际开发推荐先声明再访问变量



### 1.2 函数进阶

#### 1.2.1 函数提升

* 会把所有函数声明提升到当前作用域的最前面

* 只提升函数声明，不提升函数调用

#### 1.2.2 函数参数

* arguments 动态参数 只存在于函数里面 是伪数组

```
<script>
function getSum() {
  // console.log(arguments);
  let sum = 0
  for(let i = 0; i < arguments.length; i++) {
    sum += arguments[i]
  }
  console.log(sum);
}
getSum(2,3,4)
</script>
```

* ...是语法符号，置于最末函数形参之前，用于获取多余的实参

​	借助...获取的剩余实参，是个真数组

```
<script>
function getSum(...arr) {
  console.log(arr);
}
getSum(1,2,3)
</script>
```

* 展开运算符 (...)

```
<script>
    const arr = [1,2,3]
    console.log(...arr);

    //1.求最大值
    console.log(Math.max(...arr)); //3
    console.log(Math.max(arr)); //NaN
  
    //2.合并数组
    const arr2 = [3,4,5]
    const arr3 = [...arr, ...arr2]
    console.log(arr3);
 </script>
```



#### 1.2.3 箭头函数

```
<script>
    const fn = (x) => {
      console.log(x);
    }
    fn(1)
    //只有一个形参的时候可以省略小括号
    const fn1 = x => {
      console.log(x);
    }
    fn1(1)
    //只有一行代码的时候，我们可以省略大括号
    const fn2 = x => console.log(x);
    fn2(1)

    //有返回值的时候
    const fn3 = x => x + x 
    console.log(fn3(2)); 

    //返回对象时
    const fn4 = name => ({uname: name})
    console.log(fn4('planetes')); 
 </script>
```

以上小结:

* 箭头函数属于表达式函数，因此不存在函数提升
* 箭头函数只有一个参数时可以省略圆括号()
* 箭头函数函数体只有一行代码时可以省略花括号{},并自动作为返回值被返回
* 加括号的函数体返回对象字面量表达式



案例：利用箭头函数对数组求和

```
  <script>
    const getSum = (...arr) => {
      let sum = 0
      for(let i = 0; i < arr.length; i++) {
        sum += arr[i]
      }
      return sum
    }
    console.log(getSum(1,5,3));
  </script>
```



箭头函数中this的指向

箭头函数不会自己创建this，它只会从自己的作用域链的上一层沿用this

在开发中【使用箭头函数前需要考虑函数中 this 的值】，事件回调函数使用箭头函数时，this 为全局的 window，因此 **DOM事件回调函数为了简便，还是不太推荐使用箭头函数**

```
  <script>
    console.log(this); //this指向window
    function fn() {
      console.log(this); //window 
    }
    window.fn()

    const obj = {
      name:'chelly',
      sayHi: function () {
        console.log(this); //obj
      }
    }
    obj.sayHi()

    const fn1 = () => {
      console.log(this); //window
    }
    fn1()

    const obj1 = {
      name:'chelly',
      sayHi: () => {
        console.log(this); //window
      }
    }
    obj1.sayHi()

    const obj2 = {
      name:'chelly',
      sayHi:function () {
        let i = 0
        const count = () => {
          console.log(this); //obj2
        }
        count()
      }
    }
    obj2.sayHi()
  </script>
```



### 1.3 解构赋值

tip：是一种快速为变量赋值的简洁语法，本质上仍然是为**变量赋值**。

#### 1.3.1 数组解构

概念：数组解构是将数组的单元值**快速批量赋值**给一系列变量的简洁**语法**。

```
<script>
  const arr = [60, 80, 100]
  const [min, avg, max] = arr
  console.log(max);
</script>
```

案例：两数交换

```
<script>
  let a = 1
  let b = 2;//必须加分号！
  [a, b] = [b, a]
  console.log(a, b);
</script>
```

tip：js前面**必须加分号的情况**

* 立即执行函数

```
<script>
  (function t() { })();
</script>
```

* 数组解构

(案例：两数交换有所体现)



一些情况：

* 变量多，单元值少，undefined

```
<script>
  const [a, b, c, d] = [1, 2, 3]
  console.log(d); //undefined
</script>
```

* 变量少，单元值多

```
<script>
  const [e, f] = [1, 2, 3]
  console.log(e,f);//1 2
</script>
```

* 剩余参数 变量少 单元值更多

```
<script>
  const [a, b, ...c] = [1, 2, 3, 4]
  console.log(c); //[3,4]
</script>
```

* 防止undefined传递，设置默认值

```
<script>
  const [a = 0, b = 0] = [1]
  console.log(a,b); //1,0
</script>
```

* 按需导入赋值

```
<script>
  const [a, b, , d] = [1, 2, 3, 4]
  console.log(d); //4
</script>
```



#### 1.3.2 对象解构

对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法

```
  <script>
    const obj = {
      name: 'chelly',
      age: 18
    }
    //老方法调用name obj.name
    const { name, age } = obj
    //要求属性名和变量名必须一致

    //可以改名
    const { name:uname} = obj
    console.log(name);
    console.log(age);
    console.log(uname);
  </script>
```

解构数组对象：

```
<script>
  const sodagreen = [
    {
      name:'qingfeng',
      age:42
    },
    {
      name:'jiakai',
      age:42
    }
  ]
  const [{ name, age },{ name:name1, age:age1 }] = sodagreen
  console.log(name, name1);
</script>
```

#### 1.3.3 遍历数组foreach方法

遍历数组的每个元素

不返回值

适用遍历数组对象

```
  <script>
    const arr = ['red', 'pink', 'green']
    const result = arr.forEach(function(item, index) {
      console.log(item);
      console.log(index);
    })
  </script>
```

4.filter方法

filter()方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素

筛选数组符合条件的元素，并返回筛选之后元素的新数组

返回值：返回数组，包含了符合条件的所有元素。如果没有符合条件的元素则返回空数组

参数：currentValue 必须写， index 可选 

因为返回新数组，所以不会影响原数组

```
  <script>
    const arr = [10, 20, 30]
    const newArr = arr.filter(item => item >= 20)
    console.log(newArr);
  </script>
```

## Day2

### 2.1 深入对象

#### 2.1.1 创建对象三种方法

```
  <script>
    //1.利用字面量创建对象
    const obj = new Object()
    obj.name = 'pink'
    console.log(obj);

    //2.利用new Object创建函数
    const obj1 = new Object({ uname: 'red' })
    console.log(obj1);

    //3.利用构造函数创建对象
    function EGOIST(name, gender) {
      this.name = name
      this.gender = gender
    }
    const ryo = new EGOIST('ryo', '男')
    const chelly = new EGOIST('chelly', '女')
    console.log(chelly);
  </script>
```



#### 2.1.2 构造函数

构造函数 ：是一种特殊的函数，主要用来初始化对象

约定：

* 它们的命名以大写字母开头 
* 它们只能由 "new" 操作符来执行。

说明：

* 实例化构造函数时没有参数时可以省略 () 
* 构造函数内部无需写return，返回值即为新创建的对象 
* 构造函数内部的 return 返回的值无效，所以不要写return  
* new Object（） new Date（） 也是实例化构造函数

```
  <script>
  	function EGOIST(name, gender) {
      this.name = name
      this.gender = gender
      // 有默认返回对象
    }
    const ryo = new EGOIST('ryo', '男')
    const chelly = new EGOIST('chelly', '女')
    console.log(chelly);
  </script>
```



#### 2.1.3 实例成员&静态成员

实例成员：

通过构造函数创建的对象称为实例对象，实例对象中的**属性**和**方法**称为实例成员。

```
  <script>
    function EGOIST(name, gender) {
      this.name = name
      this.gender = gender
    }
    const chelly = new EGOIST('chelly', '女')
    chelly.song = 'planetes' //实例属性
    chelly.sing = () => {   //实例方法
      console.log('is a singer');
    }
    console.log(chelly);
  </script>
```

静态成员：

构造函数的属性和方法被称为静态成员

```
  <script>
    function EGOIST(name, gender) {
      this.name = name
      this.gender = gender
    }
    EGOIST.region = 'Japan' // 静态实例
    EGOIST.songs = function() { // 静态方法
      console.log('departure');
    }
    const chelly = new EGOIST('chelly', '女')
    console.log(chelly);
  </script>
```



### 2.2 内置构造函数

#### 2.2.1 Object

Object 是内置的构造函数，用于创建普通对象。

```
  <script>
    const user = new Object({ name:'小明', age:19 })
  </script>
```

推荐使用字面量方式声明对象，而不是 Object 构造函数

三种静态方法：

```
  <script>
    const user = { name:'小明', age:19 }
    //1.keys 获取所有的属性名
    console.log(Object.keys(user)); // ['name', 'age']  是数组
    //2.values 获取所有的属性值
    console.log(Object.values(user)); //['小明', 19] 
    //3.assign 对象的拷贝 能给对象添加属性
    const o = {}
    Object.assign(o, user)
    Object.assign(o, { gender:'男' }) //添加
    console.log(o);
  </script>
```



#### 2.2.2 Array

创建数组建议使用字面量创建，不用 Array构造函数创建

* reduce() 数组求和

```
  <script>
    const arr = [1, 5, 8]

    //1.没有初始值时
    const total1 = arr.reduce(function (prev, current) {
      return prev + current 
    })
    console.log(total1); //14

    //2.有初始值
    const total2 = arr.reduce(function (prev, current) {
      return prev + current
    }, 10)
    console.log(total2); //24

    //3.箭头函数的写法
    const total3 = arr.reduce((prev, current) => prev + current, 10)
    console.log(total3); //24
  </script>
```

* find() 查找第一个并返回该对象

```
  <script>
    const arr = ['red', 'blue', 'green']
    const re = arr.find(function (item) {
      return item === 'blue' //返回数组第一个找到的对象
    })
    console.log(re); //blue
  </script>
```

* every() 全部符合条件返回true，否则false

```
  <script>
    const arr = [10, 20, 30]
    const flag = arr.every(item => item >= 20)
    console.log(flag); //false
  </script>
```

* from() 伪数组转换为真数组

```
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script>
    const lis = document.querySelectorAll('ul li')
    //lis.pop() 报错
    const liss = Array.from(lis)
    liss.pop()
    console.log(liss);
  </script>
```



#### 2.2.3 String

* split( ) 把字符串转化为数组 和join()相反

```
  <script>
    const str = 'pink,red'
    const arr = str.split(',')
    console.log(arr); // ['pink', 'red']
  </script>
```

* substring( ) 截取字符串

```
  <script>
    const str = 'pink,red'
    const re = str.substring(1,3)
    console.log(re); //in
  </script>
```

* startsWith( ) 判断是否以指定字符串开头

```
  <script>
    const str = 'pink,red'
    const re1 = str.startsWith('pi')
    console.log(re1);//true
    const re2 = str.startsWith('in')
    console.log(re2);//false
  </script>
```

* includes( ) 判断是否包含

```
  <script>
    const str = 'pink,red'
    const re1 = str.includes('pi')
    console.log(re1);//true
    const re2 = str.includes('in')
    console.log(re2);//true
  </script>
```



#### 2.2.4 Number

* number.**toFixed**(num) number保留num位小数（四舍五入）
* 例：( 0.1 * 100 + 0.2 * 100) / 100 这样先*100再除以100可以防止精度缺失 



## Day 3

### 3.1 编程思想

#### 3.1.1 面向过程

就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次 调用就可以了

#### 3.1.2 面向对象

面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

* 在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。
* 面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。
* 特性：封装性、继承性、多态性

#### 3.1.3 两者对比

面向过程：

* 优点：性能比面向对象高，适合跟硬件联系很紧密 的东西，例如单片机就采用的面向过程编程。 
* 缺点：没有面向对象易维护、易复用、易扩展

面向对象：

* 优点：易维护、易复用、易扩展，由于面向对象有封装 、继承、多态性的特性，可以设计出低耦合的系统，使 系统 更加灵活、更加易于维护
* 缺点：性能比面向过程低

### 3.2 构造函数

* 封装：是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。
* 构造函数实例创建的对象彼此独立、互不影响

```
  <script>
    function Star(name, age) {
      this.name = name
      this.age = age
      this.sing = function () { //存在浪费内存的问题，因此需要原型对象prototype
        console.log('唱歌');
      }
    }
    const ldh = new Star('刘德华', 55)
    const zxy = new Star('张学友', 58)
  </script>
```



### 3.3 原型

#### 3.3.1 原型

* 构造函数通过原型分配的**函数**是所有对象所 **共享的**
* JavaScript 规定，每一个构造函数都有一个 prototype 属性，指向另一个对象，所以我们也称为原型对象
* 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存
* 我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。
* 构造函数和原型对象中的this 都指向 实例化的对象

```
  <script>
    function Star(name, age) {
      this.name = name
      this.age = age
    }
    Star.prototype.sing = function () {
        console.log('唱歌');
    }
    const ldh = new Star('刘德华', 55)
    const zxy = new Star('张学友', 58)
  </script>
```

原型的**本质**：一个对象，我们也称为 prototype 为原型对象

原型的**作用**：共享方法，可以把那些不变的方法，直接定义在 prototype 对象上

构造函数和原型里面的**this指向**：实例化的对象



另外：

数组的一些方法：

arr.reverse() 数组反转

arr.sum() 数组加和

#### 3.3.2 construtor属性

概念：该属性指向该原型对象的构造函数， 简单理解，就是指向我的爸爸，我是有爸爸的孩子

应用：指向该原型对象的构造函数，防止原本函数被覆盖

```
  <script>
    function Star() {
    }
    Star.prototype = {
      constructor:Star, 
      sing: function () { console.log('sing') },
      dance: function () { console.log('dance') }
    }
    console.log(Star);
  </script>
```



#### 3.3.3 对象原型

概念：对象都会有一个属性

```
 __proto__
```

 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype  原型对象的属性和方法，就是因为对象有

```
 __proto__
```

 原型的存在。

注意：

* __proto__ 是JS非标准属性
* [[prototype]]和__proto__意义相同
* 用来表明当前实例对象指向哪个原型对象prototype
* __proto__对象原型里面也有一个 constructor属性，指向创建该实例对象的构造函数

```
  <script>
    function Star() {
    }
    const ldh = new Star()
    console.log(ldh.__proto__ === Star.prototype); //true
  </script>
```

小结：

* prototype原型和对象原型__proto__里面都有constructor, 都指向创建实例对象/原型的构造函数
* __proto__属性在实例对象里面，指向原型 prototype

#### 3.3.4 原型继承

```
  <script>
    const Person = {
      eyes: 2,
      head: 1
    }
    function Woman() {}
    Woman.prototype = Person
    Woman.prototype.constructor = Woman
    const red = new Woman()
    console.log(red);
  </script>
```

存在问题：如果我们给男人添加了一个吸烟的方法，发现女人自动也添加这个方法，通过构造函数解决

```
  <script>
    function Person() {
      this.eyes = 2
      this.head = 1
    }
    function Woman() {
    }
    Woman.prototype = new Person()
    Woman.prototype.constructor = Woman
  </script>
```



#### 3.3.5 原型链

基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对 象的链状结构关系称为原型链

本质为一种查找规则

* 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
* 如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）
* 如果还没有就查找原型对象的原型（Object的原型对象）
*  依此类推一直找到 Object 为止（null）
* __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线
* 可以使用 instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上



## Day 4

### 4.1深浅拷贝

#### 4.1.1浅拷贝

首先浅拷贝和深拷贝只针对引用类型

浅拷贝：拷贝的是地址

常见方法：(只可以拷贝表层对象)

* 拷贝对象：Object.assgin()

```
  <script>
     const obj = {
        name:'pink',
        age: 18,
      }
    const o = {}
    Object.assign(o, obj)
  </script>
```

* 拷贝对象：展开运算符 {...obj}

```
  <script>
    const obj = {
      name:'pink',
      age: 18
    }
    const o = {...obj}
    o.age = 20
    console.log(o); //age:20
    console.log(obj); //age:18
  </script>
```

* 拷贝数组： Array.Prototype.concat()  **或者** [...arr]

#### 4.1.2深拷贝

深拷贝：拷贝的是对象，不是地址

1.递归函数

* 如果一个函数在内部可以调用其本身，那么这个函数就是递归函数

* 由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件 return

```
  <div></div>
  <script>
    function getTime(){
      document.querySelector('div').innerHTML = new Date().toLocaleString()
      setTimeout(getTime, 1000)
    }
    getTime()
  </script>
```

2.深拷贝代码实现

```
  <script>
    const obj = {
      name: 'pink',
      age: 18
    }
    const o = {}
    function deepCopy(newObject, oldObj) {
      for(let k in oldObj) {
        if(oldObj[k] instanceof Array) {
          newObject[k] = []
          deepCopy(newObject[k], oldObj[k])
        } else if(oldObj[k] instanceof Object) {
          newObject[k] = {}
          deepCopy(newObject[k], oldObj[k])
        } 
        else {
          newObject[k] = oldObj[k]
        }
      }
    }
    deepCopy(o, obj)
    console.log(o);
  </script>
```

3.js库lodash

_.cloneDeep(value)

```
  <script src="./lodash.min.js"></script>
  <script>
    const obj = {
      name: 'pink',
      age: 18
    }
    const o = _.cloneDeep(obj)
    console.log(o);
  </script>
```

4.利用json实现深拷贝

```
  <script>
    const obj = {
      name: 'pink',
      age: 18
    }
    const o = JSON.parse(JSON.stringify(obj))
    console.log(o);
  </script>
```

tips：1.JSON.stringify()将一个 JavaScript 对象或值转换为 JSON 字符串

​	2.JSON.parse()方法用来解析 JSON 字符串

### 4.2异常处理

* throw抛异常

```
  <script>
    function fn(x, y) {
      if (!x || !y) {
        throw new Error('参数不能为空')
      }
      return x + y
    }
    fn()
  </script>
```

会终止程序

* try /catch 捕获异常

```
  <script>
    function fn() {
      try {
        const p = document.querySelector('.p')
        p.style.color = 'red'
      } catch(err) {
        //拦截错误，提供错误信息，但不中断程序运行
        console.log(err.message);
        //return 中断程序
        return
        //或者结合 throw
        throw new Error('出错了')
      } finally {
        alert('弹出对话框')
      }
      console.log(11);
    }
    fn()
  </script>
```

* debugger

调试用的

### 4.3处理this

普通函数没有明确调用者时 this 值为 window，严格模式下没有调用者时 this 的值为 undefined

```
  <script>
    console.log(this); //window
    function fn() {
      console.log(this); //window
    }
    setTimeout(function() {
      console.log(this) //window
    }, 1000)
    document.querySelector('button').addEventListener('click', function() {
      console.log(this); //button
    })
    const obj = {
      sayHi: function () {
        console.log(this); //obj
      }
    }
    obj.sayHi()
  </script>
```

#### 4.3.1 this指向

* 箭头函数中的 this 与普通函数完全不同，也不受调用方式的影响，事实上箭头函数中并不存在 this ！

* 在开发中【使用箭头函数前需要考虑函数中 this 的值】，事件回调函数使用箭头函数时，this 为全局的 window 因此DOM事件回调函数如果里面需要DOM对象的this，则不推荐使用箭头函数
* 同样由于箭头函数 this 的原因，基于原型的面向对象也不推荐采用箭头函数

小结：

* 函数内不存在this，沿用上一级的
* 不适用构造函数，原型函数，dom事件函数等等
* 适用需要使用上层this的地方

#### 4.3.2改变this

JavaScript 中还允许指定函数中 this 的指向，有 3 个方法可以动态指定普通函数中 this 的指向：

* call( ) (了解即可)

```
  <script>
    const obj = {
      name:'pink'
    }
    function fn(x, y) {
      console.log(this);
      console.log(x + y);
    }
    fn.call(obj, 1, 2) //指向obj，x=1, y=2
  </script>
```

* apply( )

```
  <script>
    const obj = {
      age: 18
    }
    function fn(x, y) {
      console.log(this);
      console.log(x + y);//3
    }
    fn.apply(obj,[1, 2])
  </script>
```

应用：求数组最大值

```
<script>
  const arr = [1, 2, 3, 4]
  console.log(Math.max.apply(null, arr)); //利用apply
  console.log(Math.max(...arr)); //利用展开运算符
</script>
```

* bind( )  该方法不会调用函数。但是能改变函数内部this 指向

```
  <script>
    const obj = {
      age:18
    }
    function fn() {
      console.log(this);
    }
    const fun = fn.bind(obj)
    fun()
  </script>
```

应用：

```
  <button>send</button>
  <script>
    const btn = document.querySelector('button')
    btn.addEventListener('click', function() {
      this.disabled = true
      setTimeout(function () {
        this.disabled = false
      }.bind(this), 2000)
    })
  </script>
```

* 小结

相同点：都可以改变函数内部的this指向

区别点：

call 和 apply 会调用函数, 并且改变函数内部this指向. 

call 和 apply 传递的参数不一样, call 传递参数 aru1, aru2..形式 apply 必须数组形式[arg] 

bind 不会调用函数, 可以改变函数内部this指向



### 4.4性能优化

#### 4.4.1防抖(debounce)

* 所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间
* 应用场景: 搜索框输入，设定每次输入完毕n秒后发送请求，如果期 间还有输入，则从新计算时间

应用：

* lodash实现

```
  <div class="box"></div>
  <script src="./lodash.min.js"></script>
  <script>
    const box = document.querySelector('.box')
    let i = 1
    function mouseMove() {
      box.innerHTML = i++
    }
    box.addEventListener('mousemove', _.debounce(mouseMove, 500))
  </script>
```

* 手写

```
  <div class="box"></div>
  <script>
    const box = document.querySelector('.box')
    let i = 1  // 让这个变量++
    // 鼠标移动函数
    function mouseMove() {
      box.innerHTML = ++i
      // 如果里面存在大量操作 dom 的情况，可能会卡顿
    }
    // 防抖函数
    function debounce(fn, t) {
      let timeId
      return function () {
        // 如果有定时器就清除
        if (timeId) clearTimeout(timeId)
        // 开启定时器 200
        timeId = setTimeout(function () {
          fn()
        }, t)
      }
    }
    // box.addEventListener('mousemove', mouseMove)
    box.addEventListener('mousemove', debounce(mouseMove, 200))

  </script>
```



#### 4.4.2节流(throttle)

* 所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数
* 应用场景：鼠标移动，页面尺寸发生变化，滚动条滚动等开销比较 大的情况下

应用：

* lodash实现

```
  <div class="box"></div>
  <script src="./lodash.min.js"></script>
  <script>
    const box = document.querySelector('.box')
    let i = 1
    function mouseMove() {
      box.innerHTML = i++
    }
    box.addEventListener('mousemove', _.throttle(mouseMove, 500))
  </script>
```

* 手写

```
  <script>
    const box = document.querySelector('.box')
    let i = 1
    function mouseMove() {
      box.innerHTML = i++
    }
    function throttle(fn, t) {
      let timer = null
      return function() {
        if(!timer){
          timer = setTimeout(function () {
            fn()
            timer = null
          }, t)
        }
      }
    }
    box.addEventListener('mousemove', throttle(mouseMove, 500))
  </script>
```

