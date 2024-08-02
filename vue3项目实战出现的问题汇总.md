---
typora-root-url: ..\..\img
---

# vue3项目实战出现的问题汇总

## 1 找不到模块“./App.vue”或其相应的类型声明。ts(2307)

**问题如下图：**

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/notFoundApp.png)

实际上路径是存在的，只是建议出现了问题

**解决方案：**

你可以在项目的根目录下的env.d.ts文件中添加类型声明，以解决找不到模块“./App.vue”或其相应的类型声明的问题。你可以按照以下步骤进行操作：

1. 在项目的根目录下创建一个名为env.d.ts的文件。

2. 在env.d.ts文件中添加以下内容：

```
// <reference types="vite/client" />
declare module "*.vue" {
  import type { DefineComponent } from "vue"
  const vueComponent: DefineComponent<{}, {}, any>
  export default vueComponent
}
```

3. 重新启动你的开发服务器。



**原文链接**：https://blog.csdn.net/weixin_52645312/article/details/135707081



## 2 vscode触发建议缓慢问题

参考资料：

[vscode 秒出提示，增加速度效率_vscode trigger慢-CSDN博客](https://blog.csdn.net/qq_37487141/article/details/108358850)

[vscode触发建议缓慢问题_vite 在intellj代码提示很慢-CSDN博客](https://blog.csdn.net/qq_33982898/article/details/138666989)