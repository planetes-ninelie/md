# AJAX

## 1 AJAX入门

### 1.1 AJAX概念和axios使用

#### 1.1.1 概念

* AJAX是异步的JavaScript和XML
* 简单来说，就是使用XMLHttpRequest对象与服务器通信
* 它可以使用JSON,XML,HTML,text文本等格式发送和接收数据
* 异步特性，可以在不重新刷新页面的情况下与服务器通信，交换数据或更新页面

* AJAX是浏览器和服务器进行数据通信的技术

 

#### 1.1.2 axios的使用

1. 引入axios.js 

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

2. 使用axios函数，传入配置对象，再用.then回调函数接收结果，并做后续处理



案例：

```
  <div></div>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios({
      url: 'https://hmajax.itheima.net/api/province',
    }).then(result => {
      console.log(result.data.list.join('<br>'));
      document.querySelector('div').innerHTML = result.data.list.join('<br>')
    })
  </script>
```



### 1.2 认识URL

#### 1.2.1 定义

统一资源定位符，俗称网页地址，用于访问服务器资源

#### 1.2.2 组成

* 协议

http协议：超文本传输协议，规定浏览器和服务器之间传输数据的格式

以指定格式传输数据

以指定格式解析服务器返回的资源

* 域名

标记服务器在互联网的方位

* 资源路径

标记资源在服务器下的具体位置

### 1.3 URL查询参数

* 定义

浏览器提供给服务器的额外信息，让服务器返回浏览器想要的数据

* 语法

http://xxx.com/xxx?参数值1=值1&参数名2=值2

* 案例

```
  <div></div>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios({
      url: 'https://hmajax.itheima.net/api/city',
      params: {
        pname: '河北省' 
      }
    }).then(result => {
      console.log(result.data.list);
      document.querySelector('div').innerHTML = result.data.list.join('<br>')
    })
  </script>
```



### 1.4 常见请求方法和数据提交

* 请求方法

| 请求方法 | 操作             |
| -------- | ---------------- |
| GET      | 获取数据         |
| POST     | 数据提交         |
| PUT      | 修改数据（全部） |
| DELETE   | 删除数据         |
| PATCH    | 修改数据         |

* 案例：提交数据

```
  <script>
    document.querySelector('button').addEventListener('click', () => {
      axios({
        method:'post',
        url: 'https://hmajax.itheima.net/api/register',
        data: {
          username: 'planetes',
          password: '123456'
        }
      }).then(result => {
        console.log(result);
      }).catch(error => {
        alert(error.response.data.message)
      })
    })
  </script>
```



### 1.5 HTTP协议-报文

请求报文组成：

* 请求行：请求方法，URL，协议

* 请求头：以键值对的格式携带的附加信息，比如:Content-Type
* 空行：分隔请求头，空行之后的是发送服务器的资源
* 请求体：发送的资源

响应报文组成：

* 响应行（状态行）：协议、HTTP响应状态码、状态信息
* 响应头：以键值对的格式携带的附加信息，比如：Content-Type
* 空行：分隔响应头，空行之后是服务器返回的资源
* 响应体：返回的资源

HTTP响应状态码：

| 状态码 | 说明       |
| ------ | ---------- |
| 1xx    | 信息       |
| 2xx    | 成功       |
| 3xx    | 重定向消息 |
| 4xx    | 客户端错误 |
| 5xx    | 服务端错误 |



### 1.6 form-serialize

* 作用：快速收集表单元素的值
* 案例：

```
  <script>
    document.querySelector('.btn').addEventListener('click', () => {
      const form = document.querySelector('.example-form')
      /** 
      hash 设置获取数据结构
        -true js对象
        -false 查询字符串
      empty 设置是否获取空值
      */
      const data = serialize(form, { hash:true, empty: true })
      const { uname, pwd } = data
      console.log(uname, pwd);
    })
  </script>
```

## 2 AJAX综合案例

### 2.1 Bootstrap弹窗

#### 2.1.1 步骤

* 引入 bootstrap.css 和 bootstrap.js

```
  <!-- 引入bootstrap.css -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet">
```

```
<!-- 引入bootstrap.js -->
  <script src="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/5.2.3/js/bootstrap.min.js"></script>
```

* 准备弹框标签，确认结构 

网址：[Modal · Bootstrap v5 中文文档 v5.3 | Bootstrap 中文网 (bootcss.com)](https://v5.bootcss.com/docs/components/modal/)

* 通过自定义属性，控制弹框的显示和隐藏

#### 2.1.2 通过属性控制，弹框显示或隐藏

```
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target=".my-box">
    显示弹框
  </button>
```

```
<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
```

#### 2.1.3 通过 JS 控制，弹框显示或隐藏

```
  <script>
    //1.创建弹框对象
    const modelDom = document.querySelector('.name-box')
    const modal = new bootstrap.Modal(modelDom)

    document.querySelector('.edit-btn').addEventListener('click', () => {
      modal.show()
    })

    document.querySelector('.save-btn').addEventListener('click', () => {
      modal.hide()
    })
  </script>
```



### 2.2 图片上传

```
    document.querySelector('.upload').addEventListener('change', e => {
      const fd = new FormData()
      fd.append('img', e.target.files[0])
      axios({
        method:'post',
        url: `http://hmajax.itheima.net/api/uploadimg`,
        data: fd
      }).then((result) => {
        const imgURL = result.data.data.url
        console.log(result.data.data);
        document.querySelector('.my-img').src = imgURL
      }).catch((err) => {
        console.log(err);
      });
    })
```

## 3 AJAX原理

### 3.1 XMLHttpRequest

* 定义：XHR对象用于与服务器交互。通过XMLHttpRequest可以在不刷新页面的情况下请求特定URL，获取数据

* axios内部采用XMLHttpRequest与服务器交互

* 使用步骤：

  * 创建XMLHttpRequest对象
  * 配置请求方法和请求url地址
  * 监听loaded事件，接收响应结果

  ```
    <script>
      /**
       * 目标：使用XMLHttpRequest对象与服务器通信
       *  1. 创建 XMLHttpRequest 对象
       *  2. 配置请求方法和请求 url 地址
       *  3. 监听 loadend 事件，接收响应结果
       *  4. 发起请求
      */
      const xhr = new XMLHttpRequest()
      xhr.open('get','http://hmajax.itheima.net/api/province')
      xhr.addEventListener('loadend', () => {
        const data = JSON.parse(xhr.response)
        const p = document.createElement('p')
        p.innerHTML = data.list.join('<br>')
        document.body.appendChild(p)
        console.log(data);
      })
      xhr.send()
    </script>
  ```

* 查询参数

  * 定义：浏览器提供给服务器的额外信息，让服务器返回浏览器想要的数据

  * 语法：http://xxxx.com/xxx/xxx?参数名1=值1&参数名2=值2

```
  <script>
    /**
     * 目标: 根据省份和城市名字, 查询对应的地区列表
    */
    document.querySelector('button').addEventListener('click', () => {
      const pname = document.querySelector('.province').value
      const cname = document.querySelector('.city').value
      const paramsObj = new URLSearchParams({
        pname,
        cname
      })
      const queryString = paramsObj.toString()
      console.log(queryString);
      const xhr = new XMLHttpRequest()
      xhr.open('get',`http://hmajax.itheima.net/api/area?${queryString}`)
      xhr.addEventListener('loadend', () => {
        const data = JSON.parse(xhr.response).list
        document.querySelector('.list-group').innerHTML = data.map(item => {
          return `
            <li class="list-group-item">${item}</li>
          `
        }).join('<br>')
        console.log(data);
        
      })
      xhr.send()
    })
  </script>
```



* 数据提交
  * 需求：通过 XHR 提交用户名和密码，完成注册功能
  * 请求头设置 Content-Type：application/json 
  * 请求体携带 JSON 字符串

```
  <script>
    document.querySelector('.reg-btn').addEventListener('click', () => {
      const xhr = new XMLHttpRequest()
      xhr.open('post','http://hmajax.itheima.net/api/register')
      xhr.addEventListener('loadend', () => {
        console.log(xhr.response);
      })
      xhr.setRequestHeader('Content-Type', 'application/json')
      const user = { username: 'kokomisuki', password: '123456' }
      const userStr = JSON.stringify(user)
      xhr.send(userStr)
    })
  </script>
```



### 3.2 Promise

* 定义：Promise对象用于表示一个异步操作的最终完成（或失败）及其结果值	
  * 成功和失败状态，可以关联对应处理程序
  * 本身是同步的，但是then和catch回调函数是异步
  
* 简单应用：

```
  <script>
    /**
     * 目标：使用Promise管理异步任务
    */
  const p = new Promise((resolve, reject) => {
    setTimeout(() => {
      // resolve('success')
      reject(new Error('error'))
    },2000)
  })
  p.then(result => {
    console.log(result);
  }).catch(error => {
    console.log(error);
  })
  </script>
```

* 三种状态

  * 待定（pending）：初始状态，既没有被兑现，也没用被拒绝
  * 已兑现（fulfilled）：操作成功完成
  * 已拒绝（rejected）：操作失败

  tip：Promise对象一旦被兑现/拒绝 .catch(回调函数) 就是已敲定了，状态无法再被改变

```
  <p class="my-p"></p>
  <script>
    /**
     * 目标：使用Promise管理XHR请求省份列表
     *  1. 创建Promise对象
     *  2. 执行XHR异步代码，获取省份列表
     *  3. 关联成功或失败函数，做后续处理
    */
    const p = new Promise((resolve, reject) => {
      const xhr = new XMLHttpRequest()
      xhr.open('get', 'http://hmajax.itheima.net/api/province')
      xhr.addEventListener('loadend', () => {
        if (xhr.status >= 200 && xhr.status < 300) {
          resolve(JSON.parse(xhr.response))
        } else {
          reject(new Error(xhr.response))
        }
      })
      xhr.send()
    })

    p.then(re => {
      console.log(re.list.join('<br>'));
      document.querySelector('.my-p').innerHTML = re.list.join('<br>')
    }).catch(error => {
      console.log(error);
    })
  </script>
```



### 3.3 封装简易版axios

```
  <div class="my-p"></div>
  <script>
    /**
     * 目标：封装_简易axios函数_获取省份列表
     *  1. 定义myAxios函数，接收配置对象，返回Promise对象
     *  2. 发起XHR请求，默认请求方法为GET
     *  3. 调用成功/失败的处理程序
     *  4. 使用myAxios函数，获取省份列表展示
    */
    function myAxios(config) {
      return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest()
        xhr.open(config.method || 'GET', config.url)
        xhr.addEventListener('loadend', () => {
          if (xhr.status >= 200 && xhr.status < 300) {
            resolve(JSON.parse(xhr.response))
          } else {
            reject(new Error(xhr.response))
          }
        })
        xhr.send()
      })
    }
    myAxios({
      url: 'http://hmajax.itheima.net/api/province'
    }).then((result) => {
      console.log(result);
      document.querySelector('.my-p').innerHTML = result.list.join('<br>')
    }).catch((err) => {
      console.log(err);
      document.querySelector('.my-p').innerHTML = err.message
    });
  </script>
```

```
    function myAxios(config) {
      return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest()
        if (config.params) {
          const paramsObj = new URLSearchParams(config.params)
          const queryString = paramsObj.toString()
          config.url += `?${queryString}`
        }
        xhr.open(config.method || 'GET', config.url)
        xhr.addEventListener('loadend', () => {
          if (xhr.status >= 200 && xhr.status < 300) {
            resolve(JSON.parse(xhr.response))
          } else {
            reject(new Error(xhr.response))
          }
        })
        if (config.data) {
          const jsonStr = JSON.stringify(config.data) 
          xhr.setRequestHeader('Content-Type', 'application/json')
          xhr.send(jsonStr)
        } else {
          xhr.send()
        }
      })
    }
```

## 4 AJAX进阶

#### 4.1 同步代码和异步代码

* 定义：
  * 同步代码：逐行执行，需原地等待结果后，才继续向下执行 
  * 异步代码：调用后耗时，不阻塞代码继续执行（不必原地等待），在将来完成后触发一个回调函数
    * setTimeout/setInterval、事件、AJAX都是异步代码
    * 异步代码接收结果：使用回调函数

#### 4.2 回调函数地狱和Promise链式调用

* 回调函数地狱
  * 概念：在回调函数中嵌套回调函数，一直嵌套下去就形成了回调函数地狱
  * 缺点：可读性差，异常无法捕获，耦合性严重，牵一发动全身
* Promise-链式调用
  * 使用 then 方法返回新 Promise 对象特性，一直串联下去
  * 用于解决回调函数嵌套问题
  * 案例：

```
<script>
    /**
     * 目标：把回调函数嵌套代码，改成Promise链式调用结构
     * 需求：获取默认第一个省，第一个市，第一个地区并展示在下拉菜单中
    */
    let pname = ''
    axios({url: 'http://hmajax.itheima.net/api/province'}).then(result => {
      pname = result.data.list[0]
      document.querySelector('.province').innerHTML = pname
      return axios({url: 'http://hmajax.itheima.net/api/city', params: { pname }})
    }).then(result => {
      const cname = result.data.list[0]
      document.querySelector('.city').innerHTML = cname
      return axios({ url: 'http://hmajax.itheima.net/api/area', params: { pname, cname } })
    }).then(result => {
      const areaName = result.data.list[0]
      document.querySelector('.area').innerHTML = areaName
    })
  </script>
```



#### 4.3 async和await使用

* 概念：在 async 函数内，使用 await 关键字取代 then 函数，等待获取 Promise 对象成功状态的结果值
* 案例：

```
  <script>
    /**
     * 目标：掌握async和await语法，解决回调函数地狱
     * 概念：在async函数内，使用await关键字，获取Promise对象"成功状态"结果值
     * 注意：await必须用在async修饰的函数内（await会阻止"异步函数内"代码继续执行，原地等待结果）
    */

	async function getData() {
      try {
        const pObj = await axios({ url: 'http://hmajax.itheima.net/api/province' })
        const pname = pObj.data.list[0]
        const cObj = await axios({ url: 'http://hmajax.itheima.net/api/city', params: { pname } })
        const cname = cObj.data.list[0]
        const aObj = await axios({ url: 'http://hmajax.itheima.net/api/area', params: { pname, cname } })
        const areaName = aObj.data.list[0]

        document.querySelector('.province').innerHTML = pname
        document.querySelector('.city').innerHTML = cname
        document.querySelector('.area').innerHTML = areaName
      } catch (error) {
        console.dir(error);
      }  
    }
    getData()
  </script>
```

tip:console.dir()  在控制台中显示指定JavaScript对象的属性，并通过类似文件树样式的交互列表显示



#### 4.4 事件循环-EventLoop

* 概念：执行代码和收集异步任务，在调用栈空闲时，反复调用任务队列里 回调函数执行机制
* 产生原因：JavaScript 是单线程的，为了不阻塞 JS 引擎，设计执行代码的模型
* 执行过程：
  * 执行同步代码，遇到异步代码交给宿主浏览器环境执行 
  * 异步有了结果后，把回调函数放入任务队列排队
  *  当调用栈空闲后，反复调用任务队列里的回调函数
* 宏任务与微任务
  * 宏任务：浏览器执行的异步代码
    * 例如：JS 执行脚本事件，setTimeout/setInterval，AJAX请求完成 事件，用户交互事件等
  * 微任务：JS 引擎执行的异步代码
    * 例如：Promise对象.then()的回调
  * JS内如何执行：
    * 执行第一个 script 脚本事件宏任务，里面同步代码
    * 遇到 宏任务/微任务 交给宿主环境，有结果回调函数进入对应队列
    * 当执行栈空闲时，清空**微任务**队列，再执行下一个**宏任务**，从1再来

#### 4.5 Promise.all静态方法

* 概念：合并多个 Promise 对象，等待所有同时成功完成（或某一个失败），做后续逻辑
* 案例：

```
    const arr = ['110100', '310100', '440100', '440300']
    const areaPromise = arr.map(item => {
      return axios({ url:'http://hmajax.itheima.net/api/weather', params: { city: item } })
    })
    const p = Promise.all(areaPromise)
    p.then(result => {
      const htmlStr = result.map(item => {
        return `<li class="">${item.data.data.area} --- ${item.data.data.weather}</li>`
      }).join('')
      document.querySelector('.my-ul').innerHTML = htmlStr
    }).catch(err => {
      console.log(err);
    })
```



# Node.js

## 1 基本概念

* 定义：基于 Chrome 的 V8 引擎封装，独立执行 JavaScript 代码的环境
* 与浏览器环境的js最大区别：Node.js 环境中没有 BOM 和 DOM
* 作用：
  * 编写后端程序：提供数据和网页资源等
  * 前端工程化：集成各种开发中使用的工具和技术
* 如何执行代码？在 VSCode 终端中输入：node xxx.js 回车即可执行（注意路径）

## 2 fs模块

* 定义：封装了与本机文件系统进行交互的，方法和属性
* 语法：
  * 加载fs模块对象
  * 写入文件内容
  * 读取文件内容
    * 案例：

```js
const fs = require('fs')
fs.writeFile('./test1.txt', 'hello, Node.js', (err) => {
  if (err) console.log(err);
  else console.log('success');
})

fs.readFile('./test1.txt', (err, data) => {
  if (err) console.log(err);
  else console.log(data.toString());
})
```

* path路径处理
  * 问题：Node.js 代码中，相对路径是**根据终端所在路径**来查找的，可能无法找到你想要的文件
  * 解决：使用绝对路径
    * __dirname 内置变量（获取当前模块目录-绝对路径）
    * path.join() 会使用特定于平台的分隔符，作为定界符，将所有给定的路径片段连接在一起
  * 案例：

```
const fs = require('fs')
const path = require('path')
fs.readFile(path.join(__dirname,'../test1.txt'), (err, data) => {
  if (err) console.log(err);
  else console.log(data.toString());
})
```

* 案例：压缩html

```

const fs = require('fs')
const path = require('path')
fs.readFile(path.join(__dirname,'../index.html'), (err, data) => {
  if (err) console.log(err);
  else {
    const htmlStr = data.toString()
    const resultStr = htmlStr.replace(/[\r\n]/g, '')
    console.log(resultStr);
    fs.writeFile(path.join(__dirname, '../dist/index.html'), resultStr, err => {
      if (err) console.log(err);
      else console.log("success");
    })
  }
})
```

## 3 http模块

* 加载http模块，创建web服务对象
* 监听request请求事件，设置响应头和响应体

案例：

```
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => {
  res.setHeader('Content-Type', 'text/plain;charset=utf-8')
  res.end('welcome')
})

server.listen(3000, () => {
  console.log('success');
})
```

## 4 模块化

4.1 CommonJS标准

* 使用特定语法
  * 导出：module.exports = { }
  * 导入：require('模块名或路径')
* 一般应用在 Node.js 项目环境中

4.2 ECMAScript 标准 

*  默认导出和导入
  * 导出：export default {}
  * 导入：import 变量名 from '模块名或路径'
* 注意：Node.js 默认支持 CommonJS 标准语法
  * 如需使用 ECMAScript 标准语法，在运行模块所在文件夹新建 package.json 文件，并设置 { "type" : "module" }
* 一般应用在前端工程化项目中



## 5 npm

* 软件包管理器使用：
  * 初始化清单文件：npm init -y （得到 package.json 文件，有则略过此命令）
  * 下载软件包：npm i 软件包名称
  * 使用软件包：

* 安装所有依赖：
  * 下载软件包：npm i 软件包名称

* 全局软件包 nodemon：
  * 安装：npm i nodemon -g（-g 代表安装到全局环境中）
  * 运行：nodemon 待执行的目标 js 文件
* 删除软件包：npm umi 软件包名

# Webpack



# Git

1 配置用户信息

```
git config --global user.name "itheima"
git config --global user.email "itheima@itcast.cn"

```

2 git文件状态

| 文件状态      | 概念            | 场景                 |
| ------------- | --------------- | -------------------- |
| 未跟踪（U）   | 从未被Git管理过 | 新文件               |
| 新添加（A）   | 第一次被Git暂存 | 之前版本记录无此文件 |
| 未修改（" "） | 三个区域统一    | 提交缓存后           |
| 已修改（M）   | 工作区内容变化  | 修改了内容产生       |

3.本地命令

| 命令                     | 作用                       |
| ------------------------ | -------------------------- |
| git add 文件名           | 暂存指定文件               |
| git add .                | 暂存所有改动的文件         |
| git commit -m "注释说明" | 提交并保存，产生版本快照   |
| git status -s            | 查看暂存区和工作区文件状态 |
| git restore 目标文件     | 临时恢复成暂存区的代码内容 |
| git rm -cached 目标文件  | 移除暂存区已暂存的文件     |
| git reset --soft 版本号  | 回退                       |
| git reset --hard 版本号  |                            |
| git reset --mixed 版本号 |                            |
| git log                  | 查看提交历史               |
| git reflog               |                            |
|                          |                            |
| git branch 分支名        | 创建分支                   |
| git checkout 分支名      | 切换指针                   |
| git checkout master      | 切回主分支                 |
| git merge 分支名         | 合并其他分支过来           |
| git branch -d 分支名     | 删除合并后的分支指针       |

4.远程命令

| 命令                                     | 作用                                |
| ---------------------------------------- | ----------------------------------- |
| git remote add 远程仓库别名 远程仓库地址 | 本地 Git 仓库添加远程仓库原点地址   |
| git remote -v                            | 查看远程仓库地址                    |
| git remote remove 远程仓库别名           | 删除远程仓库地址                    |
| git push 远程仓库别名 本地和远程分支名   | 本地 Git 仓库推送版本记录到远程仓库 |
| git clone 远程仓库地址                   | 拷贝一个 Git 仓库到本地，进行使用   |
| git pull 远程仓库别名 分支名             | 拉取                                |
| git pull --rebase 远程仓库别名 分支名    | 拉取合并，合并没有关系的记录        |

