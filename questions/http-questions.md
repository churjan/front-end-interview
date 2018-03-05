# HTTP问题

## 目录

* [HTTP request报文结构是怎样的](#HTTP-request报文结构是怎样的)
* [HTTP response报文结构是怎样的](#HTTP-response报文结构是怎样的)
* [HTTP状态消息](#HTTP状态消息)

### HTTP request报文结构是怎样的

1. 首行是**Request-Line**包括：**请求方法**，**请求URI**，**协议版本**，**CRLF**
1. 首行之后是若干行**请求头**，包括**general-header**，**request-header**或者**entity-header**，每个一行以CRLF结束
1. 请求头和消息实体之间有一个**CRLF分隔**
1. 根据实际请求需要可能包含一个**消息实体**

一个请求报文例子如下：

```text
GET /Protocols/rfc2616/rfc2616-sec5.html HTTP/1.1
Host: www.w3.org
Connection: keep-alive
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.153 Safari/537.36
Referer: https://www.google.com.hk/
Accept-Encoding: gzip,deflate,sdch
Accept-Language: zh-CN,zh;q=0.8,en;q=0.6
Cookie: authorstyle=yes
If-None-Match: "2cc8-3e3073913b100"
If-Modified-Since: Wed, 01 Sep 2004 13:24:52 GMT

name=qiu&age=25
```

[[↑] Back to top](#HTTP问题)

### HTTP response报文结构是怎样的

1. 首行是状态行包括：**HTTP版本，状态码，状态描述**，后面跟一个CRLF
1. 首行之后是**若干行响应头**，包括：**通用头部，响应头部，实体头部**
1. 响应头部和响应实体之间用**一个CRLF空行**分隔
1. 最后是一个可能的**消息实体**

响应报文例子如下：

```text
HTTP/1.1 200 OK
Date: Tue, 08 Jul 2014 05:28:43 GMT
Server: Apache/2
Last-Modified: Wed, 01 Sep 2004 13:24:52 GMT
ETag: "40d7-3e3073913b100"
Accept-Ranges: bytes
Content-Length: 16599
Cache-Control: max-age=21600
Expires: Tue, 08 Jul 2014 11:28:43 GMT
P3P: policyref="http://www.w3.org/2001/05/P3P/p3p.xml"
Content-Type: text/html; charset=iso-8859-1

{"name": "qiu", "age": 25}
```

[[↑] Back to top](#HTTP问题)

### HTTP状态消息

1. 200：请求已成功，请求所希望的响应头或数据体将随此响应返回。
1. 302：请求的资源临时从不同的 URI 响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在 Cache-Control 或 Expires 中进行了指定的情况下，这个响应才是可缓存的。
1. 304：如果客户端发送了一个带条件的 GET 请求且该请求已被允许，而文档的内容（自上次访问以来或者根据请求的条件）并没有改变，则服务器应当返回这个状态码。304 响应禁止包含消息体，因此始终以消息头后的第一个空行结尾。
1. 403：服务器已经理解请求，但是拒绝执行它。
1. 404：请求失败，请求所希望得到的资源未被在服务器上发现。
1. 500：服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。一般来说，这个问题都会在服务器端的源代码出现错误时出现。

[[↑] Back to top](#HTTP问题)