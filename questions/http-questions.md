# HTTP问题

## 目录

* [HTTP request报文结构是怎样的](#http-request报文结构是怎样的)
* [HTTP response报文结构是怎样的](#http-response报文结构是怎样的)
* [HTTP状态消息](#http状态消息)

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

[[↑] Back to top](#http问题)

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

[[↑] Back to top](#http问题)

### HTTP状态消息

* 1XX: 一般用来判断协议更换或者确认服务端收到请求这些
  * 100: 服务端收到部分请求,若是没有拒绝的情况下可以继续传递后续内容
  * 101: 客户端请求变换协议,服务端收到确认
  * 2xx: 请求成功,是否创建链接,请求是否接受,是否有内容这些
  * 200: 请求成功
  * 201: 请求创建成功和资源创建成功
* 3XX: 一般用来判断重定向和缓存
  * 301: 所有请求已经转移到新的 url(永久重定向),会被缓存
  * 302: 临时重定向,不会被缓存
  * 304: 本地资源暂未改动,优先使用本地的(根据If-Modified-Since or If-Match去比对服务器的资源,缓存)
* 4XX: 一般用来确认授权信息,请求是否出错,页面是否丢失
  * 400: 请求出错
  * 401: 未授权,不能读取某些资源
  * 403: 阻止访问,一般也是权限问题
  * 404: 页面丢失,资源没找到
  * 408: 请求超市
  * 415: 媒介类型不被支持，服务器不会接受请求。
* 5XX: 基本都是服务端的错误
  * 500: 服务端错误
  * 502: 网关错误
  * 504: 网关超时

[[↑] Back to top](#http问题)
