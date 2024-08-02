# github搭建图床

tip：下载Watt Toolkit加速（会出现问题，因为这个搞了一小时，关掉即可）

参考资料：[如何搭建自己的图床(GitHub版)-CSDN博客](https://blog.csdn.net/qq_44231797/article/details/131658184)

[配置手册 | PicGo](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github图床)

[picgo图床报错“unable to verify the first certificate“-CSDN博客](https://blog.csdn.net/weixin_51189637/article/details/130031891?ops_request_misc=%7B%22request%5Fid%22%3A%22172068862516800188588108%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=172068862516800188588108&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-130031891-null-null.142^v100^pc_search_result_base4&utm_term=Error%3A unable to verify the first certificateat TLSSocket.onConnectSecure(node%3A tls wrap%3A1530%3A34)at TLSSocket.emit (node%3Aevents%3A394%3A28)&spm=1018.2226.3001.4187)

**1 创建github仓库**

**2 生成token令牌**

​	点击个人头像 -> Settings -> Developer settings -> 选择Tokens(classic) -> 设置Note 和Expiration -> 全选repo -> Generate token -> 复制生成的token

**3 在自己的github仓库创建分支用于存储图片**

**4 下载picgo**

在github中搜索picgo -> 下载对应的picgo安装包（Molunerfinn/PicGo）-> 点击仓库里的Releases,找到适合的安装版本

**5 在picgo配置参数**

图床设置 -> Github -> Github设置按照给的格式

**6 最后将需要上传的图片拖入picgo即可**



## **tip：如何在github上创建一个与master无关联的分支用于存放图片？**

1 打开存放图片或md文件资源的文件夹

2 `git init`初始化本地仓库

3 `git add .`

4 `git commit -m '(提交简述)'`

5 `git remote add origin 'https:xxx.git'`

6 `git push -u origin '(新的远程仓库分支名)'`