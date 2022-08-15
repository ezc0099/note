# XMLHttpRequest

发送一个 HTTP 请求，需要创建一个 XMLHttpRequest 对象，打开一个 URL，最后发送请求。当所有这些事务完成后，该对象将会包含一些诸如响应主体或 [HTTP status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) 的有用信息。

## **构造函数**：XMLHttpRequest（）

## **属性：**

### **1.XMLHttpRequest.readyState**

|      |                                     |                                                   |
| ---- | ----------------------------------- | ------------------------------------------------- |
| 值   | 状态                                | 描述                                              |
| 0    | UNSENT (unsent)                     | 代理被创建，但尚未调用 open() 方法。              |
| 1    | OPENED (opened)                     | open() 方法已经被调用。                           |
| 2    | HEADERS_RECEIVED (headers_received) | send() 方法已经被调用，并且头部和状态已经可获得。 |
| 3    | LOADING (loading)                   | 下载中；responseText 属性已经包含部分数据。       |
| 4    | DONE (done)                         | 下载操作已完成。                                  |

### **2.XMLHttpRequest.response**

响应的正文

### **3.XMLHttpRequest.status**

只读属性 XMLHttpRequest.status 返回了 XMLHttpRequest 响应中的数字状态码。status 的值是一个无符号短整型。在请求完成前，status 的值为 0。值得注意的是，如果 XMLHttpRequest 出错，浏览器返回的 status 也为 0。

同标准http状态码

### **4.XMLHttpRequest.statusText**

只读属性 XMLHttpRequest.statusText 返回了XMLHttpRequest 请求中由服务器返回的一个DOMString 类型的文本信息，这则信息中也包含了响应的数字状态码。不同于使用一个数字来指示的状态码XMLHTTPRequest.status，这个属性包含了返回状态对应的文本信息，例如"OK"或是"Not Found"。如果请求的状态readyState的值为"UNSENT"或者"OPENED"，则这个属性的值将会是一个空字符串。

如果服务器未明确指定一个状态文本信息，则statusText的值将会被自动赋值为"OK"。

### **5.XMLHttpRequest.timeout**

XMLHttpRequest.timeout 是一个无符号长整型数，代表着一个请求在被自动终止前所消耗的毫秒数。默认值为 0，意味着没有超时。**只能用在异步请求中，**在同步请求中使用会抛出一个 InvalidAccessError 类型的错误。

当超时发生， [timeout](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/timeout_event) 事件将会被触发。

## **方法：**

### 1.**XMLHttpRequest.abort()**

如果该请求已被发出，XMLHttpRequest.abort() 方法将终止该请求。当一个请求被终止，它的  readyState 将被置为0，并且请求的 status 置为 0。

### **2.XMLHttpRequest.open()**

初始化一个请求。

常用：**XHR.open(method,url,async)**

全：XHR.open(method,url,async,user,password)

除method和url外均为可选参数。

**method**：要使用的 HTTP 方法，比如 GET、POST、PUT、DELETE、等。对于非 HTTP(S) URL 被忽略。

**url**：发送请求的url。

**async**：Boolean值，表示是否异步执行，默认为true。

----如果值为 false，send() 方法直到收到答复前不会返回。如果 true，已完成事务的通知可供事件监听器使用。如果 multipart 属性为 true 则这个必须为 true，否则将引发异常。

user、password：可选的用户名和密码用于认证用途；默认为 null。

### **3.XMLHttpRequest.send()**

XMLHttpRequest.send() 方法用于发送 HTTP 请求。如果是异步请求（默认为异步请求），则此方法会在请求发送后立即返回；如果是同步请求，则此方法直到响应到达后才会返回。XMLHttpRequest.send() 方法接受一个可选的参数，其作为请求主体；如果请求方法是 GET 或者 HEAD，则应将请求主体设置为 null。

如果没有使用 setRequestHeader() 方法设置 Accept 头部信息，则会发送带有 "* / *" 的Accept 头部。

关于参数（暂时没搞懂）：

XMLHttpRequest.send(body)

body：可选参数，默认为null。表示在 XHR 请求中要发送的数据体. 可以是：

- 可以为 Document, 在这种情况下，它在发送之前被序列化。
- 为 XMLHttpRequestBodyInit, 从 [per the Fetch spec](https://fetch.spec.whatwg.org/#typedefdef-xmlhttprequestbodyinit) （规范中）可以是 Blob, BufferSource, FormData, URLSearchParams, 或者 USVString 对象。
- null

### **4.XMLHttpRequest.setRequestHeader()**

XMLHttpRequest.setRequestHeader() 是设置 HTTP 请求头部的方法。此方法必须在 open() 方法和 send() 之间调用。如果多次对同一个请求头赋值，只会生成一个合并了多个值的请求头。

语法：XHR.setRequestHeader(header, value);

header表示属性的名称，value表示属性的值。

### **5.XMLHttpRequest.getResponseHeader()**

XMLHttpRequest.getResponseHeader()方法返回包含指定响应头文本的字符串。

如果在返回的响应头中有多个一样的名称，那么返回的值就会是用逗号和空格将值分隔的字符串。getResponseHeader() 方法以 UTF 编码返回值。搜索的报文名是不区分大小写的。

**语法**：var myHeader = XMLHttpRequest.getResponseHeader(name);

**参数name**：一个字符串，表示要返回的报文项名称。

**返回值**：报文项值，如果连接未完成，响应中不存在报文项，或者被 W3C 限制，则返回 null。

### **6.XMLHttpRequest.getAllResponseHeaders()**

**XMLHttpRequest.getAllResponseHeaders()** 方法返回所有的响应头，以 CRLF 分割的字符串，或者 null 如果没有收到任何响应。 （CRLF,即CR：\r，LF:\n ）

**注意：** 对于复合请求（ multipart requests ），这个方法返回当前请求的头部，而不是最初的请求的头部。

MDN上的例子值得一看：https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/getAllResponseHeaders

## **事件：**

**abort**：当一个请求终止时 abort 事件被触发，比如程序执行 XMLHttpRequest.abort()。

事件处理程序：onabort，值为一个回调函数。

如XMLHttpRequest.onabort = callback;

**error**：当请求遇到错误时，将触发error 事件。

时间处理程序：onerror，值为一个回调函数。

如XMLHttpRequest.onerror = callback;

**load:**当一个XMLHttpRequest请求完成的时候会触发load 事件。

事件处理程序：onload，同上。

**readystatechange**：只要 readyState 属性发生变化，就会调用相应的[处理函数 (en-US)](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers)。这个回调函数会被用户线程所调用。XMLHttpRequest.onreadystatechange 会在 XMLHttpRequest 的readyState 属性发生改变时触发 readystatechange (en-US) 事件的时候被调用。

时间处理程序：onreadystatechange，同上。

**timeout**：当进度由于预定时间到期而终止时，会触发timeout事件。

事件处理程序：ontimeout，同上。