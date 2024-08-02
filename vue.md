# 1 vue核心

## 1.1 模版语块和数据绑定

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script type="text/javascript" src="../vue.js"></script> //引入vue.js
</head>
<body>
  <div id="root">
    <h1>{{name}}</h1> 
    <a v-bind:href="url">链接</a><br/> //v-bind可以省略
    <input :value="name" type="text"><br/> //单向绑定
    <input v-model="name" type="text">  //双向绑定
  </div>
  <script type="text/javascript">
    Vue.config.productionTip = false
    new Vue({
      el: '#root',
      data: {
        name: 'hello',
        url: 'https://www.bilibili.com/'
      }
    })
  </script>
</body>
</html>
```

```
  <div id="root">
    <h1>{{name}}</h1>
  </div>
  <script type="text/javascript">
    Vue.config.productionTip = false
    new Vue({
      //el: '#root', //el第一种写法

      //data第一种写法：对象式
      // data: {
      //   name: 'hello'
      // }

      //data第二种写法：函数式
      //function可以省略
      //由vue管理的函数，不能写箭头函数，否则this不再是vue实例
      data:function() {
        return {
          name: 'hello'
        }
      }
    })
    v.$mount('#root') //el第二种写法
  </script>
```



## 1.2 MVVM模型

* MVVM模型
  * M：模型（Model）：data中的数据
  * V：视图（View）：模板代码
  * VM：视图模型（ViewModel）：Vue实例
* data中所有的属性，最后都出现在vm身上
* vm身上所有属性及Vue原型上所有属性，在Vue模板中都可以直接使用



## 1.3 数据代理

* Object.defineProperty

```
  <script type="text/javascript">
    let number = 18
    let person = {
      name:'张三',
      sex:'男',
      //age:18,
      age: number
    }
    Object.defineProperty(person, 'age', {
      // value:18,
      // enumerable:true, //控制属性是否枚举 Object.keys()
      // writable:true, //控制属性是否可以被修改 person.age = 19
      // configurable:true //控制属性是否可以被删除 delete person.age 

      // 当有人读取person的age属性时，get函数就会被调用
      get() {
        return number
      },

      //当有人修改person的age属性时，set函数就会被调用
      set(value) {
        number = value
      }
    })
  </script>
```

* 通过一个对象代理对另一个对象中属性的操作

```
  <script type="text/javascript">
    let obj = {x:100}
    let obj2 = {y:200}

    Object.defineProperty(obj2, 'x', {
      get() {
        return obj.x
      },
      set(value){
        obj.x = value
      }
    })
  </script>
```



# 2 vue组件化编码

# 3 vue-ajax

# 4 vue UI组件库

# 5 vue-router

# 6 vuex

# 7 vue源码分析