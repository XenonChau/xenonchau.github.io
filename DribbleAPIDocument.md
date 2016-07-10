# Dribbble API 文档

* [概述(Overview)](#概述overview)
  * [架构(Schema)](#架构schema)
  * [参数(Parameters)](#参数parameters)
  * [客户端错误(Client Errors)](#客户端错误client-errors)
  * [HTTP动作(HTTP Verbs)](http动作http-verbs)
  * [认证(Authentication)](#认证authentication)
  * [页码(Pagination)](#页码pagination)
      * [链路报头(Link Header)] (#链路报头link-header)
  * [限流(Rate Limiting)](#限流rate-limiting)
      * [保持限流(Staying within the rate limit)] (#保持限流staying-within-the-rate-limit)
  * [条件请求(Conditional requests)](#条件请求conditional-requests)
  * [跨源资源共享(Cross Origin Resource Sharing)](#跨源资源共享cross-origin-resource-sharing)
  * [JSON-P回调(JSON-P Callbacks)](#json-p回调json-p-callbacks)
  
* [媒体类型(Media Types)](#媒体类型media-types)
  * [评论正文属性(Comment Body Property)](评论正文属性comment-body-property)
  * [Shot描述属性(Shot Description Property)](Shot描述属性shot-description-property)
  
## 概述(Overview)

请注意你必须[注册你的应用](https://dribbble.com/account/applications/new)并且在请求时使用OAuth认证或使用你的API客户端的access token进行认证。在此之前，请务必仔细阅读我们的[条款及指引](http://developer.dribbble.com/terms/)学习如何使用API。


### 架构(Schema)

所有的API访问都是通过HTTPS，从`api.dribbble.com/v1/`接口访问。所有数据都是通过JSON发送和接收的。

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

返回多个项目的请求默认将被分为每页30项。您可以使用`page`参数规定更多页面。对于一些资源，你还可以使用`per_page`参数设置高达100的自定义页面容量。请注意，由于技术原因，不是所有的接口都支持`per_page`参数。

```
$ curl "https://api.dribbble.com/v1/user/followers?page=2&per_page=100"
```

注意，省略`page`参数将返回第一页。

#### 链路报头(Link Header)

页码信息包含在[链路报头](http://tools.ietf.org/html/rfc5988)中。可能某些其它资源不根据页面数量进行分页，重要的是按照这些Link Header的值来定，而不是自己构建URL。例如，请求第二页时，可以提供以下报头：

```
Link: <https://api.dribbble.com/v1/user/followers?page=1&per_page=100>; rel="prev",
  <https://api.dribbble.com/v1/user/followers?page=3&per_page=100>; rel="next"
```
`rel` 的值可能是：

|Name	|Description|
|:-- |:--|
|next	|显示结果直属的下一个页面的URL。|
|prev	|显示结果直属的上一个页面的URL。|

### 限流(Rate Limiting)

对于使用OAuth登陆的请求，您可以设置已认证的用户最高每分钟60次，每人每天1,440次。对于使用你应用程序的客户端访问令牌(Client Access Token)那些未经授权的请求，你可以设置最高每分钟60次，每天10,000次。

你可以检查任一API请求返回的HTTP报头来查看当前每分钟限流的状态：

```
$ curl -i https://api.dribbble.com/v1/users/simplebits

HTTP/1.1 200 OK
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1392321600
The headers tell you everything you need to know about your current rate limit status:
```

Header Name	|Description
---|---
X-RateLimit-Limit	|The maximum number of requests that the consumer is permitted to make per minute.
X-RateLimit-Remaining	|The number of requests remaining in the current rate limit window.
X-RateLimit-Reset	|The time at which the current rate limit window resets in UTC epoch seconds.

如果你需要时间显示为不同的格式，任何现代编程语言可以都完成这项工作。例如，如果您在您的网页浏览器中打开控制台，就可以轻松将时间重置为一个JavaScript Date对象。

```
new Date(1392321600 * 1000)
// => Thu Feb 13 2014 14:00:00 GMT-0600 (CST)
```

一旦你超出限流，你会收到一个错误响应：

```
HTTP/1.1 429 Too Many Requests
Status: 429 Too Many Requests
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1392321600

{ "message" : "API rate limit exceeded." }
```

#### 保持限流(Staying within the rate limit)

如果你超出你的限流上限，你可以通过缓存API的响应来解决问题。如果你已经缓存，但仍然超出你的限流上限，请与我们联系，来为您的OAuth应用申请更高的限流上限。

### 条件请求(Conditional requests)

大多数响应都返回`ETag`报头。许多响应也会返回一个`Last-Modified`报头。你可以使用这些报头值(Header Value)来让使用了`If-None-Match`和`If-Modified-Since`报头的后续请求去请求这些资源。如果资源没有改变，服务器将返回一个`304 Not Modified`。

```
$ curl -i https://api.dribbble.com/v1/users/simplebits
HTTP/1.1 200 OK
ETag: "e612e16d3c4d113573edb015d8eac1d5"
Status: 200 OK
Last-Modified: Sat, 22 Feb 2014 17:10:33 GMT
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1392321600

$ curl -i https://api.dribbble.com/v1/users/simplebits -H 'If-None-Match: "e612e16d3c4d113573edb015d8eac1d5"'
HTTP/1.1 304 Not Modified
ETag: "e612e16d3c4d113573edb015d8eac1d5"
Status: 200 OK
Last-Modified: Sat, 22 Feb 2014 17:10:33 GMT
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1392321600

$ curl -i https://api.dribbble.com/v1/users/simplebits -H "If-Modified-Since: Sat, 22 Feb 2014 17:10:33 GMT"
HTTP/1.1 304 Not Modified
ETag: "e612e16d3c4d113573edb015d8eac1d5"
Status: 200 OK
Last-Modified: Sat, 22 Feb 2014 17:10:33 GMT
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1392321600
```

### 跨源资源共享(Cross Origin Resource Sharing)

本API对Ajax请求支持跨资源共享(CORS)。你可以阅读 [CORS W3C working draft](http://www.w3.org/TR/cors), 或者HTML5安全指南的 [这个简介](http://code.google.com/p/html5security/wiki/CrossOriginRequestSecurity)。

下面是从浏览器点击`http://example.com`发送请求的示例：

```
$ curl -i https://api.dribbble.com/v1/users/simplebits -H "Origin: http://example.com"
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://example.com
Access-Control-Expose-Headers: ETag, Link, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset
Access-Control-Allow-Credentials: true
```

CORS的预请求(preflight request)看起来是这样的：

```
$ curl -i https://api.dribbble.com/v1/users/simplebits -X OPTIONS -H "Origin: http://example.com" -H "Access-Control-Request-Method: GET"
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://example.com
Access-Control-Allow-Methods: OPTIONS, GET
Access-Control-Expose-Headers: ETag, Link, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset
Access-Control-Max-Age: 86400
Access-Control-Allow-Credentials: true
```

### JSON-P回调(JSON-P Callbacks)

<font size=2pt>扩展阅读: &nbsp;&nbsp;&nbsp;&nbsp;JSON-P^[\[1\]](https://zh.wikipedia.org/zh-cn/JSONP)</font>

你可以发送一个回调参数给任何GET调用来获得包裹在一个JSON函数的结果。<u>这通常是浏览器避过跨域问题想要在网页中嵌入内容时被使用的</u>^[原文](# "This is typically used when browsers want to embed content in web pages by getting around cross domain issues.") 。<u>响应包括数据输出相同的常规API，以及HTTP头的相关信息</u> ^[原文](# "The response includes the same data output as the regular API, plus the relevant HTTP Header information.")。


```
$ curl "https://api.dribbble.com?callback=bar"

bar({
  "meta" : {
    "status" : 200,
    "X-RateLimit-Limit" : 60,
    "X-RateLimit-Remaining" : 59,
    "X-RateLimit-Reset" : 1392321600,
    "Link" : [
      ["https://api.dribbble.com?page=2", { "rel" : "next" }]
    ]
  },
  "data" : {
    // ...
  }
})
```

你可以写一个JavaScript处理程序来处理这样的回调：

```
function bar(response) {
  var meta = response.meta
  var data = response.data

  console.log(meta)
  console.log(data)
}
```

HTTP报头中所有的首部(header)都是字符串类型，只有一个值得注意的例外：链路(Link)。<u>链路报头(Link Header)为你预解析为`[url, options]`元组数组</u> ^[原文](# "Link headers are pre-parsed for you and come through as an array of [url, options] tuples.")。

一个看起来像这样的链接：

```
Link: <url1>; rel="next", <url2>; rel="foo"; bar="baz"
```

… 它的回调输出看起来是这样的：

```
{
  "Link" : [
    [
      "url1",
      {
        "rel" : "next"
      }
    ],
    [
      "url2",
      {
        "rel" : "foo",
        "bar" : "baz"
      }
    ]
  ]
}
```

-----------

##媒体类型(Media Types)

* [概述(Overview)](#概述overview)
* [媒体类型(Media Types)](#媒体类型media-types)
  * [评论正文属性(Comment Body Property)](#评论正文属性comment-body-property)
  * [Shot描述属性(Shot Description Property)](#Shot描述属性shot-description-property)

自定义媒体类型用来让消费者在API中选择他们希望收到的数据格式。当你发起请求，这是根据向`Accept`报头添加下列任一类型来完成的。资源对媒体类型处理得很特别，能够独立地改变和支持他们的格式，对其他的资源则不这样。

当前版本支持且只支持`v1`，但未来可能会改变。所有Dribbble的媒体类型看起来是这样的：

```
application/vnd.dribbble.v1.param+json
```

### 评论正文属性(Comment Body Property)

The body of a comment can be written with some HTML, such as links, and may include auto-linked URLs and username mentions.

**HTML**

Returns HTML rendered from the body, which includes auto-linking URLs and username mentions. Response will include a body attribute. This is the default if you do not pass any specific media type.

```
application/vnd.dribbble.v1.html+json
```

**Text**

Returns a mostly text representation of the body, which is what we display in a textarea when a user is editing a comment. It may contain some HTML if the user provided any, but no auto-linking or mention links will be included. Response will include a body_text attribute.

```
application/vnd.dribbble.v1.text+json
```

### Shot描述属性(Shot Description Property)

The description of a shot can be written with some HTML, such as links, and may include auto-linked URLs and username mentions. The property is identical to a comment body property, apart from the property name.

**HTML**

Returns HTML rendered from the body, which includes auto-linking URLs and username mentions. Response will include a description attribute. This is the default if you do not pass any specific media type.

```
application/vnd.dribbble.v1.html+json
```

**Text**

Returns a mostly text representation of the description, which is what we display in a textarea when a user is editing a description. It may contain some HTML if the user provided any, but no auto-linking or mention links will be included. Response will include a description_text attribute.

```
application/vnd.dribbble.v1.text+json
```

