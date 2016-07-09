# Dribbble API 文档

* [概述](#概述)
  * [架构(Schema)](#架构(Schema))
  * [客户端错误(Client Errors)](#客户端错误(Client Errors))
  * [客户端错误(Client Errors)](#客户端错误(Client Errors))
  * [HTTP动作(HTTP Verbs)](#HTTP动作(HTTP Verbs))
  * [认证(Authentication)](#认证(Authentication))
  * [页码(Pagination)](页码(Pagination))
  * [限速(Rate Limiting)](限速(Rate Limiting))
  * [条件请求(Conditional requests)](条件请求(Conditional requests))
  * [跨源资源共享(Cross Origin Resource Sharing)](跨源资源共享(Cross Origin Resource Sharing))
  * [JSON-P回调(JSON-P Callbacks)](JSON-P回调(JSON-P Callbacks))

## 概述

请注意你必须[注册你的应用](https://dribbble.com/account/applications/new)并且在请求时使用OAuth认证或使用你的API客户端的access token进行认证。在此之前，请务必仔细阅读我们的[条款及指引](http://developer.dribbble.com/terms/)学习如何使用API。

### 架构(Schema)

所有的API访问都是通过HTTPS，从`api.dribbble.com/v1/`端口访问。所有数据都是通过JSON发送和接收的。

```
$ curl -i https://api.dribbble.com/v1/users/simplebits

HTTP/1.1 200 OK
Date: Thu, 13 Feb 2014 19:30:30 GMT
ETag: "def2bc69c674e5b48cd281aa12c2c8e9"
Server: nginx
Status: 200 OK
Content-Type: application/json; charset=utf-8
Cache-Control: max-age=0, private, must-revalidate
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1392321600
```

空字段包含为`null`，而不是被省略。

所有的时间戳返回ISO-8601格式：

```
YYYY-MM-DDTHH:MM:SSZ
```

### 参数(Parameters)

许多API方法都有可选参数。对于`GET`请求而言，任何未被指定为一段路径的参数可以作为一个HTTP查询字符串参数传递：

```
$ curl -i "https://api.dribbble.com/v1/users/simplebits/followers?page=2"
```

在本例中，`simplebits`的值是在路径中给`user`这个参数提供的，而`page`的值是在查询字符串中传递的。

对于`POST` , `PUT` , `DELETE`请求, 未包含在URL中的参数应使用JSON编码，其Content-Type应为`application/x-www-form-urlencoded`。


### 客户端错误(Client Errors)

在API调用接收请求主体时时有两种类型的客户端错误。

1\. 发送无效JSON。

```
Status: 400 Bad Request
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "message" : "解析JSON时出现问题."
}
```

2\. 发送无效字段。

```
Status: 422 Unprocessable Entity
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "message" : "认证失败.",
  "errors" : [
    {
      "attribute" : "主体",
      "message" : "不能为空"
    }
  ]
}
```

### HTTP动作(HTTP Verbs)

如果可能的话，每次操作API尽量的使用恰当的HTTP动作。

|动作|描述|
|:--|:--|
|GET|用于接收资源。|
|POST|用于创造资源。|
|PUT|用于更新资源，或进行自定义操作。|
|DELETE|用于删除资源。|

### 认证(Authentication)

有两种方式通过Dribbble API进行身份验证。

OAuth2 Token (在报头中发送)

```
$ curl -H "Authorization: Bearer OAUTH_TOKEN" https://api.dribbble.com/v1/user
```

OAuth2 Token (作为参数发送)

```
$ curl "https://api.dribbble.com/v1/user?access_token=OAUTH_TOKEN"
```

### 页码(Pagination)

Requests that return multiple items will be paginated to 30 items by default. You can specify further pages with the page parameter. For some resources, you can also set a custom page size up to 100 with the per_page parameter. Note that for technical reasons not all endpoints respect the per_page parameter.

```
$ curl "https://api.dribbble.com/v1/user/followers?page=2&per_page=100"
```

### 限速(Rate Limiting)

    [展开]

### 条件请求(Conditional requests)

    [展开]

### 跨源资源共享(Cross Origin Resource Sharing)

    [展开]

### JSON-P回调(JSON-P Callbacks)

<font size=2pt>扩展阅读: &nbsp;&nbsp;&nbsp;&nbsp;JSON-P^[\[1\]](https://zh.wikipedia.org/zh-cn/JSONP)</font>
    [展开]



