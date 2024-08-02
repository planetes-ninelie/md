---
typora-root-url: ..\..\img
---

### 如何将vue3打包后的静态文件部署到github pages呢？



tips：<u>1.利用vite构建的vue3项目</u>

​		   <u>2.打包的是纯前端项目</u>



**从打包前开始：**

#### 1. 修改公共路径

修改`vite.config.js`中的`base`路径

确保你的`vite.config.js`文件中`base`选项被正确设置。如果你的应用将部署在子目录下（例如：`https://yourusername.github.io/your-repo-name/`），你需要将`base`选项设置为该子目录。

```
// vite.config.js
export default {
  base: '/your-repo-name/',
};
```



tip：**在配置中使用环境变量**

vite官网：https://cn.vitejs.dev/config/

环境变量通常可以从 `process.env` 获得。

注意 Vite 默认是不加载 `.env` 文件的，因为这些文件需要在执行完 Vite 配置后才能确定加载哪一个，举个例子，`root` 和 `envDir` 选项会影响加载行为。不过当你的确需要时，你可以使用 Vite 导出的 `loadEnv` 函数来加载指定的 `.env` 文件。

```
import { defineConfig, loadEnv } from 'vite'

export default defineConfig(({ command, mode }) => {
  // 根据当前工作目录中的 `mode` 加载 .env 文件
  // 设置第三个参数为 '' 来加载所有环境变量，而不管是否有 `VITE_` 前缀。
  const env = loadEnv(mode, process.cwd(), '')
  return {
    // vite 配置
    define: {
      __APP_ENV__: JSON.stringify(env.APP_ENV),
    },
  }
})
```





**之后，有两种方式可选，**

- **其一：在github上直接主分支上部署静态文件；**

- **其二：在github上新建分支，将静态文件部署到新分支的根目录下**

- **其三：利用vite构建工具快速部署（推荐！！！）**



#### 方法一步骤：

##### 2.1 将打包构建路径改为/docs

修改`vite.config.js`中的`build`路径

```
 export default {
 	//修改构建路径
    build: {
      outDir: 'docs', // 改变输出目录
    }
 }
```

tips：<u>如果有配置会影响/docs文件夹的代码，注意进行修改</u>

以本人某项目为例：

- eslint

​			需要在忽略配置中添加 "docs"，当前最新版本的eslint直接在`eslint.config`添加

```
export default [
	ignores: [
      'docs/**',
    ],
]
```

- prettier

​			在`.prettierignore`中添加

```
/docs/*
```

- stylelint

​			在`.stylelintignore`中添加

```
/docs/*
```



##### 2.2 打包

在dos命令窗口输入：

```
npm run build 
```

**或者**npm脚本工具里点击build：

![build](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/build.png)

##### 2.3 上传到github

tip：<u>在此之前先建好远程仓库</u>

在Git Bash上：

```
git init
git add .
git commit -m '(简述提交内容)'
git remote add origin 'https://github.com/xxx(远程仓库url)'
git push origin master
```

此时已将代码提交至github上

##### 2.4 在github上部署

找到远程仓库里的Settings的Pages，设置Build and deployment：

1. Source里选择Deploy from a branch
2. Branch里选择master/docs
3. 点击save

操作如图：

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/githubDeployment.png)

#### 方法二步骤：

##### 3.1 打包

（同2.2的步骤）

在dos命令窗口输入：

```
npm run build 
```

**或者**npm脚本工具里点击build：

![build](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/build.png)

##### 3.2 将新分支上传到github

```
git init
git add .
git commit -m '(简述提交内容)'
git remote add origin 'https://github.com/xxx(远程仓库url)'
//先上传主分支master
git push origin master

//新建分支并切换
git checkout -b gh-pages
git rm -r .
cp -r dist/* .
git add .
git commit -m '(简述提交内容)'
git push origin gh-pages
```

tip：<u>为了避免“git rm -r .”删除分支内容，意外影响其他分支，应该在清空操作之前，保证其他分支已提交（commit）</u>

此时已将master和gh-pages的代码都已提交至github上

##### 3.4 在github上部署

（与2.4类似）

找到远程仓库里的Settings的Pages，设置Build and deployment：

1. Source里选择Deploy from a branch
2. Branch里选择gh-pages/(root)
3. 点击save

操作如图：

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/gh-pages.png)



#### **方法三步骤**(推荐！！)：

##### 4.1 在`package.json`文件中添加以下脚本：

```
"scripts": {
  "deploy": "gh-pages -d dist"
}
```

##### 4.2  安装gh-pages

你可以运行`npm run deploy`来将你的构建文件推送到gh-pages分支。但是，你需要先安装gh-pages包：

```
npm install --save-dev gh-pages
```

##### 4.3 设置 `.gitignore`文件

在`.gitignore`文件中，确保没有忽略`dist`目录，因为我们需要将构建的文件提交到GitHub。

##### 4.4 运行`npm run deploy`

最后，运行`npm run deploy`，它将自动将`dist`目录下的文件推送到gh-pages分支。



#### tip

搞定！收工！此时只需要等待几分钟，网页site就能访问了

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/site.png)



