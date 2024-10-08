---
typora-root-url: ..\..\img
---

# vue3个人博客静态页面搭建

## 1 项目初始化

### 1.1 利用vite初始化

vite官网：[开始 | Vite 官方中文文档 (vitejs.dev)](https://cn.vitejs.dev/guide/)

```
兼容性注意

Vite 需要 Node.js 版本 18+ 或 20+。然而，有些模板需要依赖更高的 Node 版本才能正常运行，当你的包管理器发出警告时，请注意升级你的 Node 版本。
```

本文使用pnpm（8.0.0以上）

1.安装pnpm

```
npm i -g pnpm
```

可查看pnpm版本

```
pnpm -v
```

2.用pnpm创建项目（在dos命令窗口自己选定的路径输入）

```
pnpm create vite
```

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/1-1createProject.png)



### 1.2 修改创建的初始模板

1.删除src/style.css文件

2.删除src/components/HelloWorld.vue文件

3.删除src/assets/vue.svg文件

4.更改index.html的title



### 1.3 eslint检验代码工具配置

**eslint中文官网:[检测并修复 JavaScript 代码中的问题。 - ESLint - 插件化的 JavaScript 代码检查工具](https://zh-hans.eslint.org/)**

ESLint最初是由[Nicholas C. Zakas](http://nczonline.net/) 于2013年6月创建的开源项目。它的目标是提供一个插件化的**javascript代码检测工具**

#### 1.首先安装eslint

```
pnpm i eslint -D
```

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/1-3eslintInstall.png)



#### 2 生成配置文件:.eslint.cjs

```
npx eslint --init
```

![](C:\Users\ilsdg\Desktop\vue_test\myBlog\public\src\1-3eslintInstall.png)

#### 3 vue3环境代码校验插件

```
pnpm install -D eslint-plugin-import eslint-plugin-vue eslint-plugin-node eslint-plugin-prettier eslint-config-prettier eslint-plugin-node @babel/eslint-parser
```

#### 4 `eslint.config.js`配置

借鉴了该文章：[Vue3（1）：项目初始化、项目配置、项目集成_eslint.config.js 使用import.meta.env-CSDN博客](https://blog.csdn.net/m0_73560798/article/details/137918706?ops_request_misc=%7B%22request%5Fid%22%3A%22172011463616800225518526%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=172011463616800225518526&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-137918706-null-null.142^v100^pc_search_result_base4&utm_term=eslint.config.js&spm=1018.2226.3001.4187)

```javascript
import globals from "globals";
import pluginJs from "@eslint/js";
import tseslint from "typescript-eslint";
import pluginVue from "eslint-plugin-vue";


export default [
  {files: ["**/*.{js,mjs,cjs,ts,vue}"]},
  {languageOptions: { globals: globals.browser }},
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
  ...pluginVue.configs["flat/essential"],

  {
    plugins: {
      prettier,
    },
    rules: {
      // 开启这条规则后，会将prettier的校验规则传递给eslint，这样eslint就可以按照prettier的方式来进行代码格式的校验
      'prettier/prettier': 'error',
      // eslint（https://eslint.bootcss.com/docs/rules/）
      'no-var': 'error', // 要求使用 let 或 const 而不是 var
      'no-multiple-empty-lines': ['warn', { max: 1 }], // 不允许多个空行
      'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
      'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
      'no-unexpected-multiline': 'error', // 禁止空余的多行
      'no-useless-escape': 'off', // 禁止不必要的转义字符
 
      // typeScript (https://typescript-eslint.io/rules)
      '@typescript-eslint/no-unused-vars': 'error', // 禁止定义未使用的变量
      '@typescript-eslint/prefer-ts-expect-error': 'error', // 禁止使用 @ts-ignore
      '@typescript-eslint/no-explicit-any': 'off', // 禁止使用 any 类型
      '@typescript-eslint/no-non-null-assertion': 'off',
      '@typescript-eslint/no-namespace': 'off', // 禁止使用自定义 TypeScript 模块和命名空间。
      '@typescript-eslint/semi': 'off',
 
      // eslint-plugin-vue (https://eslint.vuejs.org/rules/)
      'vue/multi-word-component-names': 'off', // 要求组件名称始终为 “-” 链接的单词
      'vue/script-setup-uses-vars': 'error', // 防止<script setup>使用的变量<template>被标记为未使用
      'vue/no-mutating-props': 'off', // 不允许组件 prop的改变
      'vue/attribute-hyphenation': 'off', // 对模板中的自定义组件强制执行属性命名样式
    }
  },

  // languageOptions：配置如何检查 js 代码
  {
    // 处理 与 JavaScript 相关的配置项
    // - ecmaVersion
    // - sourceType
    // - globals
    // - parser
    // - parserOptions
    // files: ["**/*.ts", "**/*.vue"],
    // ignores: ["**/*.config.js"],
    ignores: [
      '**/*.config.js',
      'dist/**',
      'node_modules/**',
      '!**/eslint.config.js',
    ],
    languageOptions: {
      // 定义可用的全局变量
      globals: globals.browser,
      // 扩展
      // ecmaVersion: "latest",
      // sourceType: "module",
      parser: commpnParser,
      parserOptions: {
        ecmaVersion: 'latest',
        sourceType: 'module',
        parser: '@typescript-eslint/parser',
        jsxPragma: 'React',
        ecmaFeatures: {
          jsx: true,
        }
      }
    }
  }
];
```

#### 5.在package.json中的“scripts”添加

```
    "lint": "eslint src",
    "fix": "eslint src --fix"
```

### 1.4 prettier格式化工具配置

有了eslint，为什么还要有prettier？eslint针对的是javascript，他是一个检测工具，包含js语法以及少部分格式问题，在eslint看来，语法对了就能保证代码正常运行，格式问题属于其次；

而prettier属于格式化工具，它看不惯格式不统一，所以它就把eslint没干好的事接着干，另外，prettier支持

包含js在内的多种语言。

总结起来，**eslint和prettier这俩兄弟一个保证js代码质量，一个保证代码美观。**

#### 1 安装依赖包

```
pnpm install -D eslint-plugin-prettier prettier eslint-config-prettier
```

#### 2 `.prettierrc.json`添加规则

```
{
  "singleQuote": true,
  "semi": false,
  "bracketSpacing": true,
  "htmlWhitespaceSensitivity": "ignore",
  "endOfLine": "auto",
  "trailingComma": "all",
  "tabWidth": 2
}
```

#### 3 `.prettierignore`忽略文件

```
/dist/*
/html/*
.local
/node_modules/**
**/*.svg
**/*.sh
/public/*
```

**通过pnpm run lint去检测语法，如果出现不规范格式,通过pnpm run fix 修改**



### 1.5 stylelint配置

[stylelint](https://stylelint.io/)为css的lint工具。可格式化css代码，检查css语法错误与不合理的写法，指定css书写顺序等。

我们的项目中使用scss作为预处理器，安装以下依赖：

```
pnpm add sass sass-loader stylelint postcss postcss-scss postcss-html stylelint-config-prettier stylelint-config-recess-order stylelint-config-recommended-scss stylelint-config-standard stylelint-config-standard-vue stylelint-scss stylelint-order stylelint-config-standard-scss -D
```

#### 1`.stylelintrc.cjs`**配置文件**

**官网:https://stylelint.bootcss.com/**

```
// @see https://stylelint.bootcss.com/

module.exports = {
  extends: [
    'stylelint-config-standard', // 配置stylelint拓展插件
    'stylelint-config-html/vue', // 配置 vue 中 template 样式格式化
    'stylelint-config-standard-scss', // 配置stylelint scss插件
    'stylelint-config-recommended-vue/scss', // 配置 vue 中 scss 样式格式化
    'stylelint-config-recess-order', // 配置stylelint css属性书写顺序插件,
    'stylelint-config-prettier', // 配置stylelint和prettier兼容
  ],
  overrides: [
    {
      files: ['**/*.(scss|css|vue|html)'],
      customSyntax: 'postcss-scss',
    },
    {
      files: ['**/*.(html|vue)'],
      customSyntax: 'postcss-html',
    },
  ],
  ignoreFiles: [
    '**/*.js',
    '**/*.jsx',
    '**/*.tsx',
    '**/*.ts',
    '**/*.json',
    '**/*.md',
    '**/*.yaml',
  ],
  /**
   * null  => 关闭该规则
   * always => 必须
   */
  rules: {
    'value-keyword-case': null, // 在 css 中使用 v-bind，不报错
    'no-descending-specificity': null, // 禁止在具有较高优先级的选择器后出现被其覆盖的较低优先级的选择器
    'function-url-quotes': 'always', // 要求或禁止 URL 的引号 "always(必须加上引号)"|"never(没有引号)"
    'no-empty-source': null, // 关闭禁止空源码
    'selector-class-pattern': null, // 关闭强制选择器类名的格式
    'property-no-unknown': null, // 禁止未知的属性(true 为不允许)
    'block-opening-brace-space-before': 'always', //大括号之前必须有一个空格或不能有空白符
    'value-no-vendor-prefix': null, // 关闭 属性值前缀 --webkit-box
    'property-no-vendor-prefix': null, // 关闭 属性前缀 -webkit-mask
    'selector-pseudo-class-no-unknown': [
      // 不允许未知的选择器
      true,
      {
        ignorePseudoClasses: ['global', 'v-deep', 'deep'], // 忽略属性，修改element默认样式的时候能使用到
      },
    ],
  },
}
```

#### 2`.stylelintignore`忽略文件

```
/node_modules/*
/dist/*
/html/*
/public/*
```

#### 3 运行脚本

```
"scripts": {
	"lint:style": "stylelint src/**/*.{css,scss,vue} --cache --fix"
}
```

最后配置统一的prettier来格式化我们的js和css，html代码

```
"scripts": {
    "dev": "vite --open",
    "build": "vue-tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint src",
    "fix": "eslint src --fix",
    "format": "prettier --write \"./**/*.{html,vue,ts,js,json,md}\"",
    "lint:eslint": "eslint src/**/*.{ts,vue} --cache --fix",
    "lint:style": "stylelint src/**/*.{css,scss,vue} --cache --fix"
  },
```

**当我们运行`pnpm run format`的时候，会把代码直接格式化**

### 1.6 husky配置

在上面我们已经集成好了我们代码校验工具，但是需要每次手动的去执行命令才会格式化我们的代码。如果有人没有格式化就提交了远程仓库中，那这个规范就没什么用。所以我们需要强制让开发人员按照代码规范来提交。

要做到这件事情，就需要利用husky在代码提交之前触发git hook(git在客户端的钩子)，然后执行`pnpm run format`来自动的格式化我们的代码。

#### 1 安装`husky`

```
pnpm install -D husky
```

#### 2 执行

```
npx husky-init
```

会在根目录下生成个一个.husky目录，在这个目录下面会有一个pre-commit文件，这个文件里面的命令在我们执行commit的时候就会执行

#### 3 在`.husky/pre-commit`文件添加如下命令：

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

pnpm run format
```

当我们对代码进行commit操作的时候，就会执行命令，对代码进行格式化，然后再提交。

### 1.7 commitlint配置

对于我们的commit信息，也是有统一规范的，不能随便写,要让每个人都按照统一的标准来执行，我们可以利用**commitlint**来实现。

#### 1 安装包

```
pnpm add @commitlint/config-conventional @commitlint/cli -D
```

#### 2 `commitlint.config.cjs `

添加配置文件，新建`commitlint.config.cjs`(注意是cjs)，然后添加下面的代码：

```
module.exports = {
  extends: ['@commitlint/config-conventional'],
  // 校验规则
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat',//新特性、新功能
        'fix',//修改bug
        'docs',//文档修改
        'style',//代码格式修改, 注意不是 css 修改
        'refactor',//代码重构
        'perf',//优化相关，比如提升性能、体验
        'test',//测试用例修改
        'chore',//其他修改, 比如改变构建流程、或者增加依赖库、工具等
        'revert',//回滚到上一个版本
        'build',//编译相关的修改，例如发布版本、对项目构建或者依赖的改动
      ],
    ],
    'type-case': [0],
    'type-empty': [0],
    'scope-empty': [0],
    'scope-case': [0],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
    'header-max-length': [0, 'always', 72],
  },
}
```

#### 3 在`package.json`中配置scripts命令

```
# 在scrips中添加下面的代码
{
"scripts": {
    "commitlint": "commitlint --config commitlint.config.cjs -e -V"
  },
}
```

现在当我们填写`commit`信息的时候，前面就需要带着下面的`subject`

```
'feat',//新特性、新功能
'fix',//修改bug
'docs',//文档修改
'style',//代码格式修改, 注意不是 css 修改
'refactor',//代码重构
'perf',//优化相关，比如提升性能、体验
'test',//测试用例修改
'chore',//其他修改, 比如改变构建流程、或者增加依赖库、工具等
'revert',//回滚到上一个版本
'build',//编译相关的修改，例如发布版本、对项目构建或者依赖的改动
```

#### 4 husky配置

```
npx husky add .husky/commit-msg 
```

#### 5 `commit-msg` 

在生成的commit-msg文件中添加下面的命令

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"
pnpm commitlint
```

当我们 commit 提交信息时，就不能再随意写了，必须是 git commit -m 'fix: xxx' 符合类型的才可以，**需要注意的是类型的后面需要用英文的 :，并且冒号后面是需要空一格的，这个是不能省略的**

### 1.7 强制使用pnpm包管理器工具

团队开发项目的时候，需要统一包管理器工具,因为不同包管理器工具下载同一个依赖,可能版本不一样,

导致项目出现bug问题,因此包管理器工具需要统一管理！！！

#### 1 `scritps/preinstall.js`

在根目录创建`scritps/preinstall.js`文件，添加下面的内容

```
if (!/pnpm/.test(process.env.npm_execpath || '')) {
  console.warn(
    `\u001b[33mThis repository must using pnpm as the package manager ` +
    ` for scripts to work properly.\u001b[39m\n`,
  )
  process.exit(1)
}
```

#### 2 配置命令

```
"scripts": {
	"preinstall": "node ./scripts/preinstall.js"
}
```

**当我们使用npm或者yarn来安装包的时候，就会报错了。原理就是在install的时候会触发preinstall（npm提供的生命周期钩子）这个文件里面的代码。**

### 1.8 若要部署到github Pages中

需要在`vite.config.ts`（vite构建的项目）中配置基础路径：

GitHub Pages 需要你指定一个基础路径，这个路径通常是你的 GitHub 用户名或仓库名。你需要告诉 Vite 在构建时使用这个基础路径，以便所有资源链接都能正确地指向 GitHub Pages。

```
export default defineConfig({
    if (command === 'build') {
        return {
        	base:'/your-repo-name/'
        }
	}
});
```

配置后，会遇到一些问题：public里的静态文件不会跟随打包，会找不到路径，所以尽量把那些需要解析的文件放到src/assets下



## 2 项目集成

### 2.1 集成element-plus

官网地址：[一个 Vue 3 UI 框架 | Element Plus (element-plus.org)](https://element-plus.org/zh-CN/#/zh-CN)

```
pnpm install element-plus @element-plus/icons-vue
```

**入口文件main.ts全局安装element-plus,element-plus默认支持语言英语设置为中文**

```
import ElementPlus from 'element-plus';
import 'element-plus/dist/index.css'
//@ts-ignore忽略当前文件ts类型的检测否则有红色提示(打包会失败)
import zhCn from 'element-plus/dist/locale/zh-cn.mjs'
//获取应用实例对象
const app = createApp(App)
//安装element-plus插件
app.use(ElementPlus, {
  locale: zhCn,
})
//将应用挂载到挂载点上
app.mount('#app')
```

**Element Plus全局组件类型声明**

```
// tsconfig.json
{
  "compilerOptions": {
    // ...
    "types": ["element-plus/global"]
  }
}
```

配置完毕可以测试element-plus组件与图标的使用.



### 2.2 src别名的配置

在开发项目的时候文件与文件关系可能很复杂，因此我们需要给src文件夹配置一个别名！！！

```
// vite.config.ts
import {defineConfig} from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'
export default defineConfig({
    plugins: [vue()],
    resolve: {
        alias: {
            "@": path.resolve("./src") // 相对路径别名配置，使用 @ 代替 src
        }
    }
})
```

**TypeScript 编译配置**

```
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": "./", // 解析非相对模块的基地址，默认是当前目录
    "paths": { //路径映射，相对于baseUrl
      "@/*": ["src/*"] 
    }
  }
}
```



### 2.3 环境变量的配置

**项目开发过程中，至少会经历开发环境、测试环境和生产环境(即正式环境)三个阶段。不同阶段请求的状态(如接口地址等)不尽相同，若手动切换接口地址是相当繁琐且易出错的。于是环境变量配置的需求就应运而生，我们只需做简单的配置，把环境状态切换的工作交给代码。**

开发环境（development）
顾名思义，开发使用的环境，每位开发人员在自己的dev分支上干活，开发到一定程度，同事会合并代码，进行联调。

测试环境（testing）
测试同事干活的环境啦，一般会由测试同事自己来部署，然后在此环境进行测试

生产环境（production）
生产环境是指正式提供对外服务的，一般会关掉错误报告，打开错误日志。(正式提供给客户使用的环境。)

注意:一般情况下，一个环境对应一台服务器,也有的公司开发与测试环境是一台服务器！！！

项目根目录分别添加 开发、生产和测试环境的文件!

```
.env.development
.env.production
.env.test
```

文件内容

```
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'development'
VITE_APP_TITLE = '硅谷甄选运营平台'
VITE_APP_BASE_API = '/dev-api'
```

```
NODE_ENV = 'production'
VITE_APP_TITLE = '硅谷甄选运营平台'
VITE_APP_BASE_API = '/prod-api'
```

```
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'test'
VITE_APP_TITLE = '硅谷甄选运营平台'
VITE_APP_BASE_API = '/test-api'
```

配置运行命令：package.json

```
 "scripts": {
    "dev": "vite --open",
    "build:test": "vue-tsc && vite build --mode test",
    "build:pro": "vue-tsc && vite build --mode production",
    "preview": "vite preview"
  },
```

通过import.meta.env获取环境变量

### 2.4 SVG图标配置

在开发项目的时候经常会用到svg矢量图,而且我们使用SVG以后，页面上加载的不再是图片资源,

这对页面性能来说是个很大的提升，而且我们SVG文件比img要小的很多，放在项目中几乎不占用资源。

 1 **安装SVG依赖插件**

```
pnpm install vite-plugin-svg-icons -D
```

 2 **在`vite.config.ts`中配置插件**

```
import { createSvgIconsPlugin } from 'vite-plugin-svg-icons'
import path from 'path'
export default () => {
  return {
    plugins: [
      createSvgIconsPlugin({
        // Specify the icon folder to be cached
        iconDirs: [path.resolve(process.cwd(), 'src/assets/icons')],
        // Specify symbolId format
        symbolId: 'icon-[dir]-[name]',
      }),
    ],
  }
}
```

3 **入口文件导入**

```
import 'virtual:svg-icons-register'
```

4 **svg封装为全局组件**

因为项目很多模块需要使用图标,因此把它封装为全局组件！！！

**在src/components目录下创建一个SvgIcon组件:代表如下**

```
<template>
  <div>
    <svg :style="{ width: width, height: height }">
      <use :xlink:href="prefix + name" :fill="color"></use>
    </svg>
  </div>
</template>

<script setup lang="ts">
defineProps({
  //xlink:href属性值的前缀
  prefix: {
    type: String,
    default: '#icon-'
  },
  //svg矢量图的名字
  name: String,
  //svg图标的颜色
  color: {
    type: String,
    default: ""
  },
  //svg宽度
  width: {
    type: String,
    default: '16px'
  },
  //svg高度
  height: {
    type: String,
    default: '16px'
  }

})
</script>
<style scoped></style>
```

在src文件夹目录下创建一个index.ts文件：用于注册components文件夹内部全部全局组件！！！

```
import SvgIcon from './SvgIcon/index.vue';
import type { App, Component } from 'vue';
const components: { [name: string]: Component } = { SvgIcon };
export default {
    install(app: App) {
        Object.keys(components).forEach((key: string) => {
            app.component(key, components[key]);
        })
    }
}
```

在入口文件引入src/index.ts文件,通过app.use方法安装自定义插件

```
import globalComponent from './components/index';
app.use(globalComponent);
```

### 2.5 集成sass

我们目前在组件内部已经可以使用scss样式,因为在配置styleLint工具的时候，项目当中已经安装过sass sass-loader,因此我们再组件内可以使用scss语法！！！需要加上lang="scss"

```
<style scoped lang="scss"></style>
```

接下来我们为项目添加一些全局的样式

在src/styles目录下创建一个index.scss文件，当然项目中需要用到清除默认样式，因此在index.scss引入reset.scss(该文件从npm里找)

```
@import './reset.scss'
```

在入口文件引入

```
import '@/styles/index.scss'
```

但是你会发现在src/styles/index.scss全局样式文件中没有办法使用$变量.因此需要给项目中引入全局变量$.

在style/variable.scss创建一个variable.scss文件！

在vite.config.ts文件配置如下:

```
export default defineConfig((config) => {
	css: {
      preprocessorOptions: {
        scss: {
          javascriptEnabled: true,
          additionalData: '@import "./src/styles/variable.scss";',
        },
      },
    },
	}
}
```

**`@import "./src/styles/variable.less";`后面的`;`不要忘记，不然会报错**!

配置完毕你会发现scss提供这些全局变量可以在组件样式中使用了！！！

### 2.6 mock数据

安装依赖:https://www.npmjs.com/package/vite-plugin-mock

```
npm i vite-plugin-mock@2.9.6
```

在 vite.config.js 配置文件启用插件。

```
import { defineConfig, loadEnv } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'
import { viteMockServe } from 'vite-plugin-mock'
//引入svg插件
import { createSvgIconsPlugin } from 'vite-plugin-svg-icons'
// https://vitejs.dev/config/
export default defineConfig(({ command, mode }) => {
  let env = loadEnv(mode, process.cwd())
  return {
    plugins: [
      vue(),
      //配置svg
      createSvgIconsPlugin({
        // Specify the icon folder to be cached
        iconDirs: [path.resolve(process.cwd(), 'src/assets/icons')],
        // Specify symbolId format
        symbolId: 'icon-[dir]-[name]',
      }),
      viteMockServe({
        enable: command === 'serve',
      }),
    ],
    //修改公共路径
    base: `${env.VITE_APP_BASE_API}/`,
    resolve: {
      alias: {
        '@': path.resolve('./src'), // 相对路径别名配置，使用 @ 代替 src
      },
    },
    //scss全局变量配置
    css: {
      preprocessorOptions: {
        scss: {
          javascriptEnabled: true,
          additionalData: '@import "./src/styles/variable.scss";',
        },
      },
    },
  }
})

```

在根目录创建mock文件夹:去创建我们需要mock数据与接口！！！

在mock文件夹内部创建一个user.ts文件

```
//用户信息数据
function createUserList() {
    return [
        {
            userId: 1,
            avatar:
                'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif',
            username: 'admin',
            password: '111111',
            desc: '平台管理员',
            roles: ['平台管理员'],
            buttons: ['cuser.detail'],
            routes: ['home'],
            token: 'Admin Token',
        },
        {
            userId: 2,
            avatar:
                'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif',
            username: 'system',
            password: '111111',
            desc: '系统管理员',
            roles: ['系统管理员'],
            buttons: ['cuser.detail', 'cuser.user'],
            routes: ['home'],
            token: 'System Token',
        },
    ]
}

export default [
    // 用户登录接口
    {
        url: '/api/user/login',//请求地址
        method: 'post',//请求方式
        response: ({ body }) => {
            //获取请求体携带过来的用户名与密码
            const { username, password } = body;
            //调用获取用户信息函数,用于判断是否有此用户
            const checkUser = createUserList().find(
                (item) => item.username === username && item.password === password,
            )
            //没有用户返回失败信息
            if (!checkUser) {
                return { code: 201, data: { message: '账号或者密码不正确' } }
            }
            //如果有返回成功信息
            const { token } = checkUser
            return { code: 200, data: { token } }
        },
    },
    // 获取用户信息
    {
        url: '/api/user/info',
        method: 'get',
        response: (request) => {
            //获取请求头携带token
            const token = request.headers.token;
            //查看用户信息是否包含有次token用户
            const checkUser = createUserList().find((item) => item.token === token)
            //没有返回失败的信息
            if (!checkUser) {
                return { code: 201, data: { message: '获取用户信息失败' } }
            }
            //如果有返回成功信息
            return { code: 200, data: {checkUser} }
        }
    }
]
```

**tip：**

可以使用Easy Mock，官网：[Easy Mock (mengxuegu.com)](https://mock.mengxuegu.com/)

Easy Mock 是一个可视化，并且能快速生成 **模拟数据** 的持久化服务。

此时，该接口相当于后端数据接口，可以取消跨域代理，直接发送请求。（个人理解）

### 2.7 axios二次封装

在开发项目的时候避免不了与后端进行交互,因此我们需要使用axios插件实现发送网络请求。在开发项目的时候

我们经常会把axios进行二次封装。

**安装axios：**

```
pnpm install axios
```

目的:

1:使用请求拦截器，可以在请求拦截器中处理一些业务(开始进度条、请求头携带公共参数)

2:使用响应拦截器，可以在响应拦截器中处理一些业务(进度条结束、简化服务器返回的数据、处理http网络错误)

在根目录下创建utils/request.ts

```
import axios from "axios";
import { ElMessage } from "element-plus";
//创建axios实例
let request = axios.create({
    baseURL: import.meta.env.VITE_APP_BASE_API,
    timeout: 5000
})
//请求拦截器
request.interceptors.request.use(config => {
    return config;
});
//响应拦截器
request.interceptors.response.use((response) => {
    return response.data;
}, (error) => {
    //处理网络错误
    let msg = '';
    let status = error.response.status;
    switch (status) {
        case 401:
            msg = "token过期";
            break;
        case 403:
            msg = '无权访问';
            break;
        case 404:
            msg = "请求地址错误";
            break;
        case 500:
            msg = "服务器出现问题";
            break;
        default:
            msg = "无网络";

    }
    ElMessage({
        type: 'error',
        message: msg
    })
    return Promise.reject(error);
});
export default request;
```

### 2.8 API接口统一管理

在开发项目的时候,接口可能很多需要统一管理。在src目录下去创建api文件夹去统一管理项目的接口；

比如:下面方式

```
//统一管理咱们项目用户相关的接口

import request from '@/utils/request'

import type {

 loginFormData,

 loginResponseData,

 userInfoReponseData,

} from './type'

//项目用户相关的请求地址

enum API {

 LOGIN_URL = '/admin/acl/index/login',

 USERINFO_URL = '/admin/acl/index/info',

 LOGOUT_URL = '/admin/acl/index/logout',

}
//登录接口
export const reqLogin = (data: loginFormData) =>
 request.post<any, loginResponseData>(API.LOGIN_URL, data)
//获取用户信息

export const reqUserInfo = () =>

request.get<any, userInfoReponseData>(API.USERINFO_URL)

//退出登录

export const reqLogout = () => request.post<any, any>(API.LOGOUT_URL)
```

### 2.9 路由配置

1.安装vue-router

```
pnpm install vue-router
```

2.创建视图组件views

在根目录src下创建文件夹views，在views创建文件夹404、home等展示页面

3.创建路由组件router

在根目录src下创建文件夹router，在router里创建`index.ts`

```
//index.ts
//通过vue-router插件实现模板路由配置
import { createRouter,createWebHashHistory } from 'vue-router';
//引入路由常量
import { constantRoutes } from './routes'

//创建路由器
let router = createRouter({
	//路由模式Hash
	history:createWebHashHistory(),
	routes: constantRoutes,
	//滚动行为
	scrollBehavior() {
		return {
			left:0,
			right:0
		}
	}
})

export default router;
```

接着创建`routes.ts`用于存放常量路由

```
//routes.ts

export const constantRoutes = [
		{
			path:'/',
			component:() => import('@/views/home/index.vue'),
			name:'home' //命名路由
		},
		{
			path:'/404',
			component:() => import('@/views/404/index.vue'),
			name: '404'
		},
		{
			path:'/:pathMatch(.*)*',
			redirect:'/404',
			name:'Any'
		}
	]
```

4.将`router/index.ts`导入到`main.ts`

```
//main.ts

//引入路由
import router from './router'
//调用路由
app.use(router)

```

### 2.10 仓库store搭建

1 安装pinia

```
pnpm i pinia
```

2 创建`sotre/index.ts`

```
//sotre/index.ts

//引入pinia
import { createPinia } from 'pinia';
//创建大仓库
let pinia = createPinia()

export default pinia
```

 3 在`main.ts`引入`sotre/index.ts`

```
//main.ts

//引入store
import pinia from './store'
//安装仓库
app.use(pinia)
```

4 创建小仓库

在`store/modules`里创建需要的小仓库

example：

```
//创建用户相关的小仓库
import { defineStore } from 'pinia'
//创建用户小仓库
let userUserStore = defineStore('User', {
	//小仓库存储数据地方
	state:() => {
		return {}
	},
	//异步|逻辑的地方
	actions: {
	
	},
	getters: {
	
	}
})
//对外暴露获取小仓库
export default userUseStore
```

## 3  静态页面搭建

### 3.1 首页

1 创建`layout/index.vue`页面

```
<template>
  <div class="layout_container">
    <div class="top">
      <top></top>
    </div>
    <div class="content">
      <content></content>
    </div>
  </div>
</template>
```

2 设置全局css变量

在`styles/variable.scss`中（在`styles/index.scss`引入）

```
//项目提供scss全局变量
//左侧菜单宽度
$base-menu-width: 260px
```

3 修改路由`router/routes.ts`

```
  {
    //首页
    path: '/',
    component: () => import('@/layout/index.vue'),
    name: 'layout',
    meta: {
      title: 'layout',
      icon: 'Avatar',
    },
    redirect: '/home',
    children: [
      {
        path: '/home',
        component: () => import('@/views/home/index.vue'),
        meta: {
          title: '首页',
          icon: 'HomeFilled',
        },
      },
    ],
  },
```

