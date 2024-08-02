# 图解Http

## 1 了解Web及网络基础

### 1.1 使用 HTTP 协议访问 Web

web页面如何呈现：

![](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/20240716154842.png)

通过发送请求获取服务器资源的 Web 浏览器等，都可称为**客户端（client）**

*也就是说客户端可以是web浏览器*

更具体的图是：

![image-20240716155014841](https://fastly.jsdelivr.net/gh/planetes-ninelie/assets/image-20240716155014841.png)

Web 使用一种名为 **HTTP**（HyperText Transfer Protocol，**超文本传输协议** ）的协议作为规范，完成从**客户端**到**服务器端**等一系列运作流程。 而协议是指规则的约定。可以说，**Web 是建立在 HTTP 协议上通信的**。

### 1.2 HTTP 的诞生

#### 1.2.1 web概念

最初设想的基本理念是：借助**多文档之间相互关联形成**的**超文本** （HyperText），连成**可相互参阅**的 **WWW**（World Wide Web，万维网）

现在已提出了 3 项 WWW 构建技术：

- **HTML**：HyperText Markup Language，超文本标记语言。把 **SGML**（Standard  Generalized Markup Language，标准通用标记语言）作为页面的文本标 记语言
- **HTTP**：作为文档传递协议
- **URL**：Uniform Resource  Locator，统一资源定位符，指定文档所在地址的 URL

关于**WWW**，是 Web 浏览器当年用来浏览超文本的**客户端应用程序时**的**名称**。现在则用来表示这一系列的集合，也可简称为 **Web**。

*也就是说web就是由html、http、url组成，分别代表着：内容、规则、地址。*

#### 1.2.2 web的历史

| 时间         | 研发者                             | 内容                                                         |
| ------------ | ---------------------------------- | ------------------------------------------------------------ |
| 1990年11月   | CERN（欧洲核子研究组织）           | 研发了世界上**第一台 Web 服务器**和 **Web 浏览器**           |
| 1992 年 9 月 | 日本                               | 日本第一个主页：[日本最初のホームページ (ibarakiken.gr.jp)](https://www.ibarakiken.gr.jp/www/) |
| 1990 年      | 众人                               | 对 HTML 1.0 草案进行讨论后**废弃**：[w3.org/MarkUp/draft-ietf-iiir-html-01.txt](https://www.w3.org/MarkUp/draft-ietf-iiir-html-01.txt) |
| 1993 年 1 月 | NCSA（美国国家超级计算机应用中心） | 发明了**Mosaic**，它以 in-line（内联）等形式显示 HTML 的图像 |
| 1993 年秋    |                                    | Mosaic 的 Windows 版和 Macintosh 版面世                      |
| 1993年左右   |                                    | NCSA Web 服务器：http://archive.ncsa.illinois.edu/mosaic.html |
| 1993年左右   |                                    | NCSA HTTPd 1.0：http://web.archive.org/web/20090426182129/http://hoohoo.ncsaillinois.edw/(原址已失效) |
|              |                                    |                                                              |

#### 1.2.3 驻足不前的 HTTP

| 名称     | 内容                                                         |
| -------- | ------------------------------------------------------------ |
| HTTP/0.9 | HTTP 于 1990 年问世。那时的 HTTP 并没有作为正式的标准被建立。 这时的 HTTP 其实含有 HTTP/1.0 之前版本的意思，因此被称为 HTTP/0.9 |
| HTTP/1.0 | HTTP 正式作为标准被公布是在 1996 年的 5 月，版本被命名为 HTTP/1.0，并记载于 RFC1945。虽说是初期标准，但该协议标准至今仍 被广泛使用在服务器端。<br />RFC1945 - Hypertext Transfer Protocol -- HTTP/1.0 http://www.ietf.org/rfc/rfc1945.txt |
| HTTP/1.1 | 1997 年 1 月公布的 HTTP/1.1 是目前主流的 HTTP 协议版本。当初的标准是 RFC2068，之后发布的修订版 RFC2616 就是当前的最新版本。<br />RFC2616 - Hypertext Transfer Protocol -- HTTP/1.1 http://www.ietf.org/rfc/rfc2616.txt |

可见，作为 Web 文档传输协议的 HTTP，它的**版本几乎没有更新**。新一 代 **HTTP/2.0 正在制订中**，但要达到较高的使用覆盖率，仍需假以时日。

当年 HTTP 协议的出现主要是为了解决文本传输的难题。由于协议本身非常简单，于是在此基础上设想了很多应用方法并投入了实际使用。现在 HTTP 协议已经超出了 Web 这个框架的局限，被运用到了各种场景里。

### 1.3 网络基础 TCP/IP









### 1.4 与 HTTP 关系密切的协议：IP、TCP 和 DNS



### 1.5 负责域名解析的 DNS 服务



### 1.6 各种协议与 HTTP 协议的关系



### 1.7 URI 和 URL



## 2 简单的 HTTP协议



## 3 HTTP报文内的 HTTP信息



## 4 返回结果的 HTTP状态码



## 5 与 HTTP协作的Web服务器



## 6 HTTP首部



## 7 确保Web安全的 HTTPS



## 8 确认访问用户身份的认证



## 9 基于 HTTP的功能追加协议



## 10 构建Web内容的技术



## 11 Web的攻击技术



