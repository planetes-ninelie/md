# 由vue-router联想到的问题

## 1 路由模式hash与history的区别（未完待续）

|                     | hash模式 | history模式 |
| ------------------- | -------- | ----------- |
| 直观上              | url带“#” | url不带“#”  |
| SEO（搜索引擎优化） | 不利于   |             |
| 浏览器兼容          | IE8以上  | IE10以上    |

tips：

- vue-router有三种模式（第三种是memory模式），而这两种比较常用

- 两者差别主要在显示形式和部署上
- 无论实现是哪种模式，最后都是监听popState事件触发路由跳转处理
- 为什么需要路由？既要让访问的URL路径变化，又不触发物理HTML页面重新加载。普通的超链接方式不能同时满足这两点

原理：

- hash模式

1. 利用锚点技术重写URL路径，会在原有的URL的路径后拼接“/#/xxx”，这种方式可以不重新加载原有的HTML页面的情况下，实现URL的切换。
2. 利用的是纯静态模式，解决了单页面应用的页码划分。
3. 它可以在不触发网页重新加载的情况下切换URL路径，配合`onhashchange()`实现，一旦URL的hash部分发生变化，就触发函数通知，通过js变成可以快速实现DOM对象的切换展示。
4. 存在问题：hash模式上URL路径只能存在一个#，在分布式微前端项目中，嵌套的子应用和主应用都会用hash模式时，会导致子应用和主应用在定义URL路径上存在困难。

- history模式

1. 不需要借助锚点技术重写URL路径，故不存在#
2. 采用history对象中的`pushState()`函数重写URL路径
3. 虽然history可重写URL路径，但重写的新路径不包含原有HTML物理文件的访问地址，所以history模式在重写URL路径后，一旦刷新网页会出现404无法访问的效果。在开发环境中，VueCli解决该问题；但在生产环境中，还需要配合生产服务器的转发规则重写。

## 2 router和route

- router作为路由器实例，即`createRouter()` 返回的对象；在选项式 API 中，它可以通过 `this.$router` 来访问。
- route作为当前路由，通过 `useRoute()` 或 `this.$route` 来访问

## 3 选项式API和组合式API

- 两种不同的书写风格
- 选项式API

```
<script>
export default {
  // data() 返回的属性将会成为响应式的状态
  // 并且暴露在 `this` 上
  data() {
    return {
      count: 0
    }
  },

  // methods 是一些用来更改状态与触发更新的函数
  // 它们可以在模板中作为事件处理器绑定
  methods: {
    increment() {
      this.count++
    }
  },

  // 生命周期钩子会在组件生命周期的各个不同阶段被调用
  // 例如这个函数就会在组件挂载完成后被调用
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>
```

- 组合式API

```
<script setup>
import { ref, onMounted } from 'vue'

// 响应式状态
const count = ref(0)

// 用来修改状态、触发更新的函数
function increment() {
  count.value++
}

// 生命周期钩子
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>
```

- 联系：选项式API是组合式API实现的
- 区别：

1. 选项式API以“组件实例”的概念为中心，类似于类
2. 组合式API核心思想是直接在函数作用域内定义响应式状态变量，并将从多个函数中得到的状态组合起来处理复杂问题



## 4 RouterView和RouterLink

- 默认全局注册

组件 `RouterView` 和 `RouterLink` 都是[全局注册](https://cn.vuejs.org/guide/components/registration.html#global-registration)的，因此它们不需要在组件模板中导入。但你也可以通过局部导入它们，例如 `import { RouterLink } from 'vue-router'`。

- 格式

在模板中，组件的名字可以是 PascalCase 风格或 kebab-case 风格的。Vue 的模板编译器支持两种格式，因此 `<RouterView>` 和 `<router-view>` 通常是等效的。

- 在DOM内模板

如果使用 DOM 内模板，那么需要[注意](https://cn.vuejs.org/guide/essentials/component-basics.html#in-dom-template-parsing-caveats)：组件名字必须使用 kebab-case 风格且不支持自闭合标签。因此你不能直接写 `<RouterView />`，而需要使用 `<router-view></router-view>`。

- 区别：

1. RouterView是用于渲染匹配的路由组件
2. RouterLink是创建导航链接



## 资料来源：

[不同的历史模式 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/essentials/history-mode.html)

[【JS基础】hash和history模式_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Er4y127zd/?spm_id_from=333.337.search-card.all.click&vd_source=2f39d3b02dd3b8ed82cb330fc996c30b)

[12.history模式和hash模式的区别_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1GB4y1R7r6/?spm_id_from=333.788.recommend_more_video.-1&vd_source=2f39d3b02dd3b8ed82cb330fc996c30b)

[＜router-view＞ 和 ＜router-link＞的区别_router-link和router-view区别-CSDN博客](https://blog.csdn.net/qq_53348178/article/details/139239846?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-139239846-blog-135702948.235^v43^control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-139239846-blog-135702948.235^v43^control&utm_relevant_index=2)

[入门 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/#组件-API-风格)

[简介 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/introduction#api-styles)