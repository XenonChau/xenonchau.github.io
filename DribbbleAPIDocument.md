# Dribbble API 文档

* [概述(Overview)](#概述overview)
  * [架构(Schema)](#架构schema)
  * [参数(Parameters)](#参数parameters)
  * [客户端错误(Client Errors)](#客户端错误client-errors)
  * [HTTP动作(HTTP Verbs)](#http动作http-verbs)
  * [认证(Authentication)](#认证authentication)
  * [页码(Pagination)](#页码pagination)
      * [链路报头(Link Header)] (#链路报头link-header)
  * [限流(Rate Limiting)](#限流rate-limiting)
      * [保持限流(Staying within the rate limit)] (#保持限流staying-within-the-rate-limit)
  * [条件请求(Conditional requests)](#条件请求conditional-requests)
  * [跨源资源共享(Cross Origin Resource Sharing)](#跨源资源共享cross-origin-resource-sharing)
  * [JSON-P回调(JSON-P Callbacks)](#json-p回调json-p-callbacks)
  
* [媒体类型(Media Types)](#媒体类型media-types)
  * [评论正文属性(Comment Body Property)](#评论正文属性comment-body-property)
  * [快照描述属性(Shot Description Property)](#快照描述属性shot-description-property)
  
* [开放授权(OAuth)](#开放授权oauth)
  * [Web应用流(Web Application Flow)](#web应用程序流web-application-flow)
  * [客户端流(Client Flow)](#客户端流client-flow)
  * [非Web应用流(Non-Web Application Flow)](#非web应用流non-web-application-flow)
  * [重定向URL(Redirect URLs)](#重定向url-redirect-urls)
  * [域(Scopes)](#域scopes)
  * [认证请求常见错误(Common errors for the authorization request)](#认证请求常见错误common-errors-for-the-authorization-request)
  * [访问令牌请求常见错误(Common errors for the access token request)](#访问令牌请求常见错误common-errors-for-the-access-token-request)
  
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
X-RateLimit-Limit	|允许该客户每分钟发出请求的最大数目。
X-RateLimit-Remaining	|当前限流窗口的剩余请求数量。
X-RateLimit-Reset	|当前限流窗口的重置时间。从UTC纪元开始。(1970-01-01 00:00:00 UTC)

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

扩展阅读: JSON-P<sup>[wikipedia](https://zh.wikipedia.org/zh-cn/JSONP)</sup>

你可以发送一个回调参数给任何GET调用来获得包裹在一个JSON函数的结果。这通常是浏览器避过跨域问题想要在网页中嵌入内容时被使用的。响应包括和常规API相同的数据输出，外加HTTP头的相关信息。


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

HTTP报头中所有的头(header)都是字符串类型，只有一个值得注意的例外：链路(Link)。链路报头(Link Header)为你预解析为`[url, options]`元组数组。

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
* [开放授权(OAuth)](#开放授权oauth)

自定义媒体类型用来让消费者在API中选择他们希望收到的数据格式。当你发起请求，这是根据向`Accept`报头添加下列任一类型来完成的。资源对媒体类型处理得很特别，能够独立地改变和支持他们的格式，对其他的资源则不这样。

当前版本支持且只支持`v1`，但未来可能会改变。所有Dribbble的媒体类型看起来是这样的：

```
application/vnd.dribbble.v1.param+json
```

### 评论正文属性(Comment Body Property)

评论正文可使用HTML编写，例如链接，并可以包含自动链接(auto-linked)的URL和用户名提及(username mentions)。

**HTML**

返回HTML从包含了自动链接(auto-linked)的URL和用户名提及(username mentions)的正文呈现。回应将包含一个`body`属性。如果你没传过任何特定的媒体类型，这就是默认值。

```
application/vnd.dribbble.v1.html+json
```

**Text**

当用户正在编辑评论时，返回一个显示在文本区域、大多是文本形式的正文。它就可能包含一些用户自己写的HTML代码，但自动链接(auto-linked)或提及(mentions)链接将被不包括在内。响应将包括一个`body_text`属性。

```
application/vnd.dribbble.v1.text+json
```

### 快照描述属性(Shot Description Property)

> 我不知道怎么翻译`Shot`，可能是“快照”。

快照描述可使用HTML编写，比如链接，并可以包括自动链接(auto-linked)的URL和用户名提及(username mentions)。该属性和评论正文属性除了名称其它都是一样的。

**HTML**

返回HTML从包含了自动链接(auto-linked)的URL和用户名提及(username mentions)的描述呈现。回应将包含一个`description`属性。如果你没传过任何特定的媒体类型，这就是默认值。

```
application/vnd.dribbble.v1.html+json
```

**Text**

当用户正在编辑描述时，返回一个显示在文本区域、大多是文本形式的描述。它就可能包含一些用户自己写的HTML代码，但自动链接(auto-linked)或提及(mentions)链接将被不包括在内。响应将包括一个`description_text`属性。

```
application/vnd.dribbble.v1.text+json
```

----------

## 开放授权(OAuth)

* [概述(Overview)](#概述overview)
* [媒体类型(Media Types)](#媒体类型media-types)
* [开放授权(OAuth)](#开放授权oauth)
  * [Web应用流(Web Application Flow)](#web应用程序流web-application-flow)
    * [1. 重定向用户请求访问Dribbble](#1-重定向用户请求访问dribbble)
    * [2. Dribbble重定向回你的站点](#2-dribbble重定向回你的站点)
    * [3. 用访问令牌来访问API](#3-用访问令牌来访问api)
  * [客户端流(Client Flow)](#客户端流client-flow)
  * [非Web应用流(Non-Web Application Flow)](#非web应用流non-web-application-flow)
  * [重定向URL(Redirect URLs)](#重定向url-redirect-urls)
  * [域(Scopes)](#域scopes)
  * [认证请求常见错误(Common errors for the authorization request)](#认证请求常见错误common-errors-for-the-authorization-request)
    * [应用挂起(Application Suspended)](#应用挂起application-suspended)
    * [重定向URI不匹配(Redirect URI Mismatch)](#重定向uri不匹配redirect-uri-mismatch)
    * [拒绝访问(Access Denied)](#拒绝访问access-denied)
  * [访问令牌请求常见错误(Common errors for the access token request)](#访问令牌请求常见错误common-errors-for-the-access-token-request)
    * [不正确的客户端凭证(Incorrect Client Credentials)](#不正确的客户端凭证-incorrect-client-credentials)
    * [重定向URI不匹配(Redirect URI Mismatch)](#重定向uri不匹配redirect-uri-mismatch)
    * [错误的验证码(Bad Verification Code)](#错误的验证码bad-verification-code)

OAuth2是一种协议，允许外部应用请求授权获得用户在Dribbble帐户内除密码外的私人信息。这比基本认证更优秀，因为令牌可以被限制为特定类型的数据，并且用户可以随时撤销它。

所有开发者需要在开始之前[注册他们的应用](https://dribbble.com/account/applications/new)。已注册的OAuth的应用分配一个唯一的客户端ID(clientID)和客户端密钥(client secret)。不要向别人分享你的客户端密钥(client secret)。

###Web应用流(Web Application Flow)

#####1. 重定向用户请求访问Dribbble

```
GET https://dribbble.com/oauth/authorize
```

**参数**

Name	|Type	|Description
----|----|----
client_id	|string	|**必须**。 你**[注册](https://dribbble.com/account/applications/new)**时即可获得一个客户端ID。
redirect_uri	|string	|用户授权之后会转到这个URL。 详情请见： **[重定向URL](#重定向url-redirect-urls)**。
scope	|string	|使用空格进行分隔的**[域](#域scopes)**列表。如果没有提供，域默认为向那些不具有有效应用令牌的用户提供公开域。对于已经拥有该应用有效令牌的用户，用户将不会显示带有域列表的授权页面。取而代之的是，流(flow)这步骤将自动和该被用户在用户最后一次完成的流(flow)的同一个的域内完成。
state	|string	|一个难以猜测的随机字符串。用于防止***跨站请求伪造***攻击。

#####2. Dribbble重定向回你的网站

Dribbble重定向回您的网站在`code`参数临时代码，以及你在上一步中`state`参数中提供的状态。如果状态不匹配，则已经由第三方和进程创建的请求应该被中止。

交换(Exchange)这个来获取访问令牌：

```
POST https://dribbble.com/oauth/token
```

**参数**

Name	|Type	|Description
----|----|----
client_id	|string	|**必须**。 你**[注册](https://dribbble.com/account/applications/new)**时即可获得一个客户端ID。
client_secret	|string	|**必须**。 你**[注册](https://dribbble.com/account/applications/new)**时即可获得一个客户端密钥。
code	|string	|**必须**。 你在**[第1步](#1-重定向用户请求访问dribbble)**的响应里会获得code。
redirect_uri	|string	|用户授权之后会转到这个URL。 详情请见： **[重定向URL](#重定向url-redirect-urls)**。

**响应**

响应将返回为以下格式的JSON：

```
{
  "access_token" : "29ed478ab86c07f1c069b1af76088f7431396b7c4a2523d06911345da82224a0",
  "token_type" : "bearer",
  "scope" : "public write"
}
```

#####3. 用访问令牌来访问API

访问令牌允许您代表用户请求API。

```
GET https://api.dribbble.com/v1/user?access_token=...
```

你可以传递如上所示的令牌中的查询参数，但更干净的做法是将其包含在Authorization标头中：

```
Authorization: Bearer ACCESS_TOKEN
```

举个栗子，在`curl`中你可以像这样设置Authorization标头：

```
curl -H "Authorization: Bearer ACCESS_TOKEN" https://api.dribbble.com/v1/user
```

###客户端流(Client Flow)

应用提供了可用于对一个服务器实现或公共JavaScript客户端的只读访问令牌。请注意，访问令牌依然受制于**[限流](#限流rate-limiting)**。

和**[使用Web访问令牌](#3-用访问令牌来访问api)**一样使用本访问令牌。

###非Web应用流(Non-Web Application Flow)

我们目前不支持OAuth的以外的任何其他身份验证方法。如果你只需要只读访问的话，试试**[客户端流](#客户端流client-flow)**。

###重定向URL(Redirect URLs)

此`redirect_uri`是可选参数。如果忽略该参数，Dribbble将用户重定向到在OAuth应用设置中配置的回调URL。如果提供该参数，重定向URL的主机和端口必须与回调URL相匹配。重定向URL路径必须引用回调URL的子目录。

```
CALLBACK: http://example.com/path

GOOD: http://example.com/path
GOOD: http://example.com/path/subdir/other
GOOD: myapplication://phone-callback
BAD:  http://example.com/
BAD:  http://example.com/bar
BAD:  http://example.com:8080/path
BAD:  http://oauth.example.com:8080/path
BAD:  http://example.org
BAD:  ssh://example.com
```

###域(Scopes)
作用域让你指定正是你需要什么类型的访问。范围限制的OAuth令牌访问。他们不授予超出其用户已经有任何额外的许可。

对于Web流，请求作用域将被显示到用户的授权表单上。

Name	|Description
   -----|------
public	|授予只读公共信息访问。<br/>`如果没提供域，这就是默认域。`
write	|授予用户资源的写权限，除评论(comment)和快照(shot)。
comment	|授予创建，更新和删除评论的完全访问权限。
upload	|授予创建，更新和删除照片和附件的完全访问权限。

您的应用可以在初始重定向中请求域(scopes)。您可以用空格分隔它们来指定多个域：

```
https://dribbble.com/oauth/authorize?
  client_id=...&
  scope=public+write
```

###认证请求常见错误(Common errors for the authorization request)

有几件事情会在为用户获取OAuth令牌的过程中可能会出错。在初始授权请求阶段，这些都是一些你可能会看到错误：

#####应用挂起(Application Suspended)

如果你设置的OAuth应用被挂起（由于滥用汇报，垃圾邮件或API的不当使用），Dribbble将重定向到使用以下包含参数错误总结的已注册过的回调URL：

```
http://your-application.com/callback?error=application_suspended
  &error_description=Your+application+has+been+suspended.
  &state=xyz
```

请**[联系技术支持](https://dribbble.com/contact?api)**来解决被挂起的应用的问题。

#####重定向URI不匹配(Redirect URI Mismatch)

如果你提供了一个和你的应用注册不匹配的`redirect_uri`，Dribbble将重定向到使用以下包含参数错误总结的已注册过的回调URL：

```
http://your-application.com/callback?error=invalid_redirect_uri
  &error_description=The+redirect+uri+included+is+not+valid.
  &state=xyz
```

要纠正这个错误，要么提供一个与你注册过的相匹配的`redirect_uri`，要么略去这个参数来使用你的应用程序注册的默认值。

#####拒绝访问(Access Denied)

如果用户拒绝访问你的应用，ribbble将重定向到使用以下包含参数错误总结的已注册过的回调URL：

```
http://your-application.com/callback?error=access_denied
  &error_description=The+resource+owner+or+authorization+server+denied+the+request.
  &state=xyz
```

~~你除了哔狗~~你什么都干不了，因为用户~~就是爹~~用不用你的应用是他的自由。通常情况下，用户就是要关闭窗口或按自己的浏览器的后退键~~怎么着啊你打我啊~~，所以看起来你可能永远都看不到这个错误。

###访问令牌请求常见错误(Common errors for the access token request)

在一个交换访问令牌代码的第二阶段，还有另外一组可能出现的错误。

#####不正确的客户端凭证(Incorrect Client Credentials)

如果`client_id`和/或`client_secret`传递不正确，您将收到此错误响应。

```
{
  "error" : "invalid_client",
  "error_description" : "Client authentication failed due to unknown client, no client authentication included, or unsupported authentication method."
}
```

为了解决这个错误，回溯并确保你有你的OAuth应用正确的凭证。仔细检查`client_id`和`client_secret`以确保它们是正确的，并且被正确的传递到Dribbble。

#####重定向URI不匹配(Redirect URI Mismatch)

如果你提供了一个和你的应用注册不匹配的`redirect_uri`，Dribbble将重定向到使用以下包含参数错误总结的已注册过的回调URL：

```
{
  "error" : "invalid_grant",
  "error_description" : "The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client."
}
```

要纠正这个错误，要么提供一个与你注册过的相匹配的`redirect_uri`，要么略去这个参数来使用你的应用程序注册的默认值。

#####错误的验证码(Bad Verification Code)

如果你传的验证码不正确、过期了或不匹配你在身份验证请求的第一阶段获得的验证码，您将会收到此错误。

```
{
  "error" : "invalid_grant",
  "error_description" : "The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client."
}
```

为了解决这个错误，重新开始OAuth流程来得到一个新的代码。

