# 计算机网络/浏览器

## HTTP和HTTPS

## HTTP报文结构

HTTP报文可以分为起始行（请求行/状态行）、请求头/响应头、空行、请求体/响应体

#### 1.请求报文

请求行：方法+路径+ http版本

```text
GET /home HTTP/1.1
```

请求头：由多个属性组成，格式为："属性名 : 属性值"

*   1\.  字段名不区分大小写

*   2\.  字段名不允许出现空格，不可以出现下划线`_`

*   3\.  字段名后面必须**紧接着**​

常见的有：

```text
Client-IP：提供了运行客户端的机器的IP地址
From：提供了客户端用户的E-mail地址
Host：给出了接收请求的服务器的主机名和端口号
Referer：提供了包含当前请求URI的文档的URL
UA-Color：提供了与客户端显示器的显示颜色有关的信息
UA-CPU：给出了客户端CPU的类型或制造商
UA-OS：给出了运行在客户端机器上的操作系统名称及版本
User-Agent：将发起请求的应用程序名称告知服务器
Accept：告诉服务器能够发送哪些媒体类型
Accept-Charset：告诉服务器能够发送哪些字符集
Accept-Encoding：告诉服务器能够发送哪些编码方式
Accept-Language：告诉服务器能够发送哪些语言
TE：告诉服务器可以使用那些扩展传输编码
Expect：允许客户端列出某请求所要求的服务器行为
Range：如果服务器支持范围请求，就请求资源的指定范围
Cookie：客户端用它向服务器传送数据
Cookie2：用来说明请求端支持的cookie版本

```

#### 2.响应报文

状态行：http版本+状态码 +状态描述

```json
HTTP/1.1 200 OK
```

响应头：与请求头一样，由多个属性组成，格式为："属性名 : 属性值"

*   1\.  字段名不区分大小写

*   2\.  字段名不允许出现空格，不可以出现下划线`_`

*   3\.  字段名后面必须**紧接着**​

常见的有：

```纯文本
Age：(从最初创建开始)响应持续时间
Public：服务器为其资源支持的请求方法列表
Retry-After：如果资源不可用的话，在此日期或时间重试
Server：服务器应用程序软件的名称和版本
Title：对HTML文档来说，就是HTML文档的源端给出的标题
Warning：比原因短语更详细一些的警告报文
Accept-Ranges：对此资源来说，服务器可接受的范围类型
Vary：服务器会根据这些首部的内容挑选出最适合的资源版本发送给客户端
Proxy-Authenticate：来自代理的对客户端的质询列表
Set-Cookie：在客户端设置数据，以便服务器对客户端进行标识
Set-Cookie2：与Set-Cookie类似
WWW-Authenticate：来自服务器的对客户端的质询列表

```

## URI URL URN

| 标识符 | 全称                                            | 作用             |
| ------ | ----------------------------------------------- | ---------------- |
| URI    | Uniform Resource Identifier<br />同意资源标识符 | 唯一标识资源     |
| URL    | Uniform Resource Locator<br />统一资源定位符    | 唯一定位资源位置 |
| URN    | Uniform Resource Name<br />统一资源名称         | 唯一识别资源     |

### 三者差异

URI 能唯一表示资源，URL 则是以资源路径来表示资源，URN 则是根据名称来表示资源

**URI 格式:**
首先先来看看 URI，根据维基百科，URI 通常表示成下列形式：

```纯文本
[协议名]://[用户名]:[密码]@[主机名]:[端口号]/[路径]?[查询参数]#[片段ID]

```

URI 可以说是 URL 和 URN 的超集，能表示的资源范围比 URL 广的许多

**URL格式：**

```纯文本
标准格式：
[协议类型]://[服务器位置IP]:[端口]/[资源层级路径][资源名称]?[查询参数]#[片段ID]

完整格式:
[协议类型]://[存取凭证]@[服务器位置IP]:[端口]/[资源层级路径][资源名称]?[查询参数]#[片段ID]

```

**常见的url格式:**

```纯文本
https://zh.wikipedia.org:443/w/index.php?title=Special:random
https                -> 协议类型
zh.wikipedia.org     -> 服务器位置（需要进行域名解析）
443                  -> 服务端口号
/w/index.php         -> 资源路径
title=Special:random -> 请求参数，形如 key=value 的键值对
```

**URN格式**:

最后一个 URN 标识符，常见于论文索引，格式如下

```纯文本
urn:[NID]:[NSS]
```

## HTTP请求方法

| 方法    | 说明                                     | HTTP版本支持 |
| ------- | ---------------------------------------- | ------------ |
| GET     | 获取资源                                 | 1.0、1.1     |
| POST    | 提交数据                                 | 1.0、1.1     |
| PUT     | 修改数据                                 | 1.0、1.1     |
| HEAD    | 获取报文首部                             | 1.0、1.1     |
| DELETE  | 删除资源                                 | 1.0、1.1     |
| OPTIONS | 列出可对资源实行的请求方法，用来跨域请求 | 1.1          |
| TRACE   | 追踪请求-响应的传输路径                  | 1.1          |
| CONNECT | 建立连接隧道，用于代理服务器             | 1.1          |

#### GET：获取资源

GET方法用来请求访问已被URI识别的资源。指定的资源经服务器解析后返回响应内容。也就是说，如果请求的资源是文本，那就原样返回；如果是像CGI（Common Gateway Interface，通用网关接口）那样的程序，则返回经过执行后的输出结果。

#### Post：传输实体主体

POST方法用于传输实体的主体。

#### PUT：传输文件

PUT方法用来传输文件，该方法要求在请求报文的主体中包含文件内容，然后保存到qingqiuURI指定的位置。如果URI不存在，则要求服务器根据请求创建资源。如果存在，服务器就接受请求内容，并修改URI资源的原始版本。

但是，由于HTTP/1.1的PUT方法自身不带验证机制，任何人都可以上传文件，存在安全性问题，因此一般不使用该方法。

#### HEAD：获取保温首部

HEAD方法和GET方法一样，只是响应中不包含报文主题部分。常用于确认URI的有效性及资源更新的日期时间等。

#### DELETE：删除文件

DELETE方法用来删除文件，是和PUT方法相反的方法。DELETE方法按请求URI删除指定的资源。

但是。HTTP/1.1的DELETE方法本身和PUT方法一样不带验证机制，所以一般也不使用。

#### OPTIONS：询问支持的方法

OPTIONS方法用来查询针对请求URI指定的资源支持的方法。

响应中服务器支持的方法存放于Allow字段中。

#### TRACE：追踪路径

客户端通过TRACE方法可以查询出发出去的请求被哪些代理服务器加工修改的。

发送请求时，在Max-Forwards首部字段中填入数值，每经过一个服务器端就将该数字减一，当数值减到0的时候就停止继续传输。

TRACE方法本就不常用，再加上它容易引发XST（Cross-Site Tracing，跨站追踪）攻击，通常就更不会用到了。

#### CONNECT：要求用隧道协议连接代理

CONNECT方法要求在与代理服务器通信时建立隧道，实现用隧道协议进行TCP通信。主要使用SSL（SecureSocketsLayer，安全套接层）和TLS（TransportLayerSecurity，传输层安全）协议把通信内容加密后经网络隧道传输。

CONNECT方法的格式： CONNECT  代理服务器名:端口号   HTTP版本

#### GET和POST的区别

#### POST和PUT的区别

## HTTP状态码

|     | 类别                     | 原因短语          |
| --- | ---------------------- | ------------- |
| 1XX | Informational(信息性状态码)  | 接受的请求正在处理     |
| 2XX | Success（成功状态码）         | 请求正常处理完毕      |
| 3XX | Redirection（重定向状态码）    | 需要进行附加操作以完成请求 |
| 4XX | Client Error（客户端错误状态码） | 服务器无法处理请求     |
| 5XX | Server Reeor（服务器错误状态码） | 服务器处理请求出错     |

常见状态码：

```纯文本
100: Continue 
继续。客户端应继续其请求。
101: Switching Protocols 
切换协议。服务器根据客户端的请求切换协议。
只能切换到更高级的协议，例如，切换到HTTP的新版本协议。
如在HTTP升级为WebSocket的时候，如果服务器同意变更，就会发送状态码 101。
```

```纯文本
200:OK 
请求成功。一般用于GET与POST请求
201:Created 
已创建。成功请求并创建了新的资源
202:Accepted 
已接受。已经接受请求，但未处理完成
203:Non-Authoritative Information 
非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
204:No Content 
无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
205:Reset Content 
重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。
可通过此返回码清除浏览器的表单域。
206:Partial Content 
部分内容。服务器成功处理了部分GET请求，
它的使用场景为 HTTP 分块下载和断点续传，当然也会带上相应的响应头字段Content-Range。
```

```纯文本
300:Multiple Choices 
多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端选择（如浏览器）
301:Moved Permanently 
永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。
今后任何新的请求都应使用新的URI代替
302:Found 
临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
303:See Other 
查看其它地址。与301类似。使用GET和POST请求查看
304:Not Modified 
未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。
客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
协商缓存命中时会返回304，304虽然是3开头但是和重定向没有什么关系
305:Use Proxy 
使用代理。所请求的资源必须通过代理访问
306:Unused 
已经被废弃的HTTP状态码
307: Temporary Redirect 
临时重定向。与302类似。使用GET请求重定向
```

```纯文本
400:Bad Request 
客户端请求的语法错误，服务器无法理解
401:Unauthorized 
请求要求用户的身份认证
402:Payment Required 
保留，将来使用
403:Forbidden 
服务器理解请求客户端的请求，但是服务器禁止访问，原因有很多，比如法律禁止、信息敏感。
404:Not Found 
服务器无法根据客户端的请求找到资源（网页）。
通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
405:Method Not Allowed 
客户端请求中的方法被禁止
406:Not Acceptable 
服务器无法根据客户端请求的内容特性完成请求
407:Proxy Authentication Required 
请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
408:Request Time-out 
服务器等待客户端发送的请求时间过长，超时
409:Conflict 
服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
410:Gone 
客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，
网站设计人员可通过301代码指定资源的新位置。
411: Length Required 
服务器无法处理客户端发送的不带Content-Length的请求信息
412: Precondition Failed 
客户端请求信息的先决条件错误
413: Request Entity Too Large 
由于请求的实体过大，服务器无法处理，因此拒绝请求。
为防止客户端的连续请求，服务器可能会关闭连接。
如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息
414: Request-URI Too Large 
请求的URI过长（URI通常为网址），服务器无法处理
415: Unsupported Media Type 
服务器无法处理请求附带的媒体格式
416: Requested range not satisfiable 
客户端请求的范围无效
417: Expectation Failed 
服务器无法满足Expect的请求头信息
429: Too Many Request
客户端发送的请求过多。
431: Request Header Fields Too Large
请求头的字段内容太大。

```

```纯文本
500: Internal Server Error 服务器内部错误，无法完成请求
501: Not Implemented 服务器不支持请求的功能，无法完成请求
502: Bad Gateway 作为网关或者代理工作的服务器尝试执行请求时，
从远程服务器接收到了一个无效的响应
503: Service Unavailable 由于超载或系统维护，服务器暂时的无法处理客户端的请求。
延时的长度可包含在服务器的Retry-After头信息中
504: Gateway Time-out 充当网关或代理的服务器，未及时从远端服务器获取请求
505: HTTP Version not supported 服务器不支持请求的HTTP协议的版本，无法完成处理
```

## 浏览器本地存储

浏览器的本地存储主要分为`Cookie`、`WebStorage`和`IndexDB`, 其中`WebStorage`又可以分为`localStorage`和`sessionStorage`。

#### Cookie

`Cookie` 最开始被设计出来其实并不是来做本地存储的，而是为了弥补`HTTP`在**状态管理上的不足**。

`HTTP` 协议是一个无状态协议，客户端向服务器发请求，服务器返回响应，故事就这样结束了，但是下次发请求如何让服务端知道客户端是谁呢？

这种背景下，就产生了 `Cookie`.

Cookie 本质上就是浏览器里面存储的一个很小的文本文件，内部以键值对的方式来存储(在chrome开发者面板的`Application`这一栏可以看到)。向同一个域名下发送请求，都会携带相同的 Cookie，服务器拿到 Cookie 进行解析，便能拿到客户端的状态。

**Cookie 的工作过程**

会用到两个字段：响应头字段 `Set-Cookie` 和请求头字段 `Cookie`。

- 响应报文使用 `Set-Cookie` 字段发送“`key=value`”形式的 `Cookie` 值
- 请求报文里用 `Cookie` 字段发送多个 `Cookie` 值



Cookie 的作用很好理解，就是用来做**状态存储**的，但它也是有诸多致命的缺陷的：

1.  容量缺陷。Cookie 的体积上限只有`4KB`，只能用来存储少量的信息。
2.  性能缺陷。Cookie 紧跟域名，不管域名下面的某一个地址需不需要这个 Cookie ，请求都会携带上完整的 Cookie，这样随着请求数的增多，其实会造成巨大的性能浪费的，因为请求携带了很多不必要的内容。
3.  安全缺陷。由于 Cookie 以纯文本的形式在浏览器和服务器中传递，很容易被非法用户截获，然后进行一系列的篡改，在 Cookie 的有效期内重新发送给服务器，这是相当危险的。另外，在`HttpOnly`为 false 的情况下，Cookie 信息能直接通过 JS 脚本来读取。

**Cookie 的属性**

**`Cookie` 的生存周期**：可以使用 `Expires` 和 `Max-Age` 两个属性来设置

- `Expires`即过期时间，用的是绝对时间点，可以理解为“截止日期”（`deadline`）。
- `Max-Age`用的是相对时间，单位是秒，浏览器用收到报文的时间点再加上 `Max-Age`，就可以得到失效的绝对时间。
- `Expires` 和 `Max-Age` 可以同时出现，浏览器会优先采用 `Max-Age` 计算失效期。

**`Cookie` 的作用域**：让浏览器仅发送给特定的服务器和 `URI`，避免被其他网站盗用。

- `Domain` 和 `Path` 指定了 `Cookie` 所属的域名和路径，浏览器在发送 `Cookie` 前会从 `URI` 中提取出 `host` 和 `path` 部分，对比 `Cookie` 的属性。
- 如果不满足条件，就不会在请求头里发送 `Cookie`。

**`Cookie` 的安全性**：尽量不要让服务器以外的人看到。

- `HttpOnly`：`Cookie` 只能通过浏览器 HTTP 协议传输，禁止其他方式访问，比如不能通过 JS 访问 `Cookie`，减少 XSS 攻击；
- `SameSite`：`SameSite` 可以防范 XSRF（跨站请求伪造）攻击，设置成 `SameSite=Strict` 可以严格限定 `Cookie` 不能随着跳转链接跨站发送，而 `SameSite=Lax` 则略宽松一点，允许 `GET`/`HEAD` 等安全方法，但禁止 `POST` 跨站发送
- `Secure`：表示这个 `Cookie` 仅能用 HTTPS 协议加密传输，明文的 HTTP 协议会禁止发送。

**Cookie使用示例**

```
// 读取网站下所有的 cookie 信息，获取的结果是一个以分号`;`作为分割的一个字符串
let allCookies = document.cookie;

// 往原来的已经存在的 cookie 中加入新的 cookie
document.cookie ="name=vincent";

// 还可以在后面加上可选择的选项键值对，如 domain、path、expires
document.cookie="name=vincent;domain=.test.com"

// 删除cookie，就是让这个 cookie 的 expires 过期，即设置这个 expires 的值为 0
document.cookie="name=vincent;domain=.test.com;expires=0");
```

https://juejin.cn/post/6844904034181070861 "https://juejin.cn/post/6844904034181070861")

#### localStorage

存储在本地，除非手动清除，否则一直存在

存储大小5M

默认不参与和服务器的通信

#### SessionStorage

在当前网页会话下有效，刷新后依然存在，但关闭页面或浏览器后就会被清除

存储大小5M

默认不参与和服务器的通信

#### indexedDB

除非被清理，否则一直存在

数据存储大小无限制

不参与和服务端的通信

**indexedDB使用示例**

```
// 使用 indexedDB.open() 方法创建或打开数据库
var request = window.indexedDB.open(dbName, version); // 数据库名 版本号
// error 事件表示打开数据库失败
request.onerror = function (event) {
  console.log('创建或打开数据库失败');
};
// success 事件表示成功打开数据库
var db;
request.onsuccess = function (event) {
  db = request.result;
  console.log('创建或打开数据库成功');
};
```

强缓存和协商缓存

认证 cookie、session、token、jwt

[https://sanyuan0704.top/blogs/perform/001.html#cache-control](https://sanyuan0704.top/blogs/perform/001.html#cache-control "https://sanyuan0704.top/blogs/perform/001.html#cache-control")

[https://juejin.cn/post/6857287743966281736#heading-21](https://juejin.cn/post/6857287743966281736#heading-21 "https://juejin.cn/post/6857287743966281736#heading-21")

[https://juejin.cn/post/6844904100035821575#heading-17](https://juejin.cn/post/6844904100035821575#heading-17 "https://juejin.cn/post/6844904100035821575#heading-17")
