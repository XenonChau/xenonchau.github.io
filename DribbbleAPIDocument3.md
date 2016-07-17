# Dribbble API 文档

## 快照

* [列出全部快照(List shots)](#列出全部快照list-shots)
* [获取快照(Get a shot)](#获取快照get-a-shot)
* [创建快照(Create a shot)](#创建快照create-a-shot)
* [更新快照(Update a shot)](#更新快照update-a-shot)
* [删除快照(Delete a shot)](#删除快照delete-a-shot)

### 列出全部快照(List shots)

```
GET /shots
```

**参数**

参数名	|类型	|描述
----|----|----
list	|string	|用下列值来限定特定类型的结果：<br/>• 动画(animated)<br/>• 附件(attachments)<br/>• 新增(debuts)<br/>• 转发集(playoffs)<br/>• 相关作品(rebounds)<br/>• 团队(teams)<br/>**默认**：所有类型的结果。
timeframe	|string	|用下列值来限定一段时间内的结果：<br/>• 周(week)<br/>• 月(month)<br/>• 年(year)<br/>• 所有时间(ever)<br/>注意，用"最新的"(recent)排序时这个值将被忽略。<br/>**默认**：从当前时间开始的返回结果。
date	|date	|限制时间范围到一个特定日期、周、月或年。必须以YYYY-MM-DD的格式。
sort	|string	|可能具有以下值的排序字段：<br/>• 评论数(comments)<br/>• 最新的(recent)<br/>• 查看数(views)<br/>**默认**: 结果按流行程度排列。

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
[
  {
    "id" : 471756,
    "title" : "Sasquatch",
    "description" : "<p>Quick, messy, five minute sketch of something that might become a fictional something.</p>",
    "width" : 400,
    "height" : 300,
    "images" : {
      "hidpi" : null,
      "normal" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch.png",
      "teaser" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch_teaser.png"
    },
    "views_count" : 4372,
    "likes_count" : 149,
    "comments_count" : 27,
    "attachments_count" : 0,
    "rebounds_count" : 2,
    "buckets_count" : 8,
    "created_at" : "2012-03-15T01:52:33Z",
    "updated_at" : "2012-03-15T02:12:57Z",
    "html_url" : "https://dribbble.com/shots/471756-Sasquatch",
    "attachments_url" : "https://api.dribbble.com/v1/shots/471756/attachments",
    "buckets_url" : "https://api.dribbble.com/v1/shots/471756/buckets",
    "comments_url" : "https://api.dribbble.com/v1/shots/471756/comments",
    "likes_url" : "https://api.dribbble.com/v1/shots/471756/likes",
    "projects_url" : "https://api.dribbble.com/v1/shots/471756/projects",
    "rebounds_url" : "https://api.dribbble.com/v1/shots/471756/rebounds",
    "animated" : false,
    "tags" : [
      "fiction",
      "sasquatch",
      "sketch",
      "wip"
    ],
    "user" : {
      "id" : 1,
      "name" : "Dan Cederholm",
      "username" : "simplebits",
      "html_url" : "https://dribbble.com/simplebits",
      "avatar_url" : "https://d13yacurqjgara.cloudfront.net/users/1/avatars/normal/dc.jpg?1371679243",
      "bio" : "Co-founder &amp; designer of <a href=\"https://dribbble.com/dribbble\">@Dribbble</a>. Principal of SimpleBits. Aspiring clawhammer banjoist.",
      "location" : "Salem, MA",
      "links" : {
        "web" : "http://simplebits.com",
        "twitter" : "https://twitter.com/simplebits"
      },
      "buckets_count" : 10,
      "comments_received_count" : 3395,
      "followers_count" : 29262,
      "followings_count" : 1728,
      "likes_count" : 34954,
      "likes_received_count" : 27568,
      "projects_count" : 8,
      "rebounds_received_count" : 504,
      "shots_count" : 214,
      "teams_count" : 1,
      "can_upload_shot" : true,
      "type" : "Player",
      "pro" : true,
      "buckets_url" : "https://dribbble.com/v1/users/1/buckets",
      "followers_url" : "https://dribbble.com/v1/users/1/followers",
      "following_url" : "https://dribbble.com/v1/users/1/following",
      "likes_url" : "https://dribbble.com/v1/users/1/likes",
      "shots_url" : "https://dribbble.com/v1/users/1/shots",
      "teams_url" : "https://dribbble.com/v1/users/1/teams",
      "created_at" : "2009-07-08T02:51:22Z",
      "updated_at" : "2014-02-22T17:10:33Z"
    },
    "team" : {
      "id" : 39,
      "name" : "Dribbble",
      "username" : "dribbble",
      "html_url" : "https://dribbble.com/dribbble",
      "avatar_url" : "https://d13yacurqjgara.cloudfront.net/users/39/avatars/normal/apple-flat-precomposed.png?1388527574",
      "bio" : "Show and tell for designers. This is Dribbble on Dribbble.",
      "location" : "Salem, MA",
      "links" : {
        "web" : "http://dribbble.com",
        "twitter" : "https://twitter.com/dribbble"
      },
      "buckets_count" : 1,
      "comments_received_count" : 2037,
      "followers_count" : 25011,
      "followings_count" : 6120,
      "likes_count" : 44,
      "likes_received_count" : 15811,
      "members_count" : 7,
      "projects_count" : 4,
      "rebounds_received_count" : 416,
      "shots_count" : 91,
      "can_upload_shot" : true,
      "type" : "Team",
      "pro" : false,
      "buckets_url" : "https://dribbble.com/v1/users/39/buckets",
      "followers_url" : "https://dribbble.com/v1/users/39/followers",
      "following_url" : "https://dribbble.com/v1/users/39/following",
      "likes_url" : "https://dribbble.com/v1/users/39/likes",
      "members_url" : "https://dribbble.com/v1/teams/39/members",
      "shots_url" : "https://dribbble.com/v1/users/39/shots",
      "team_shots_url" : "https://dribbble.com/v1/users/39/teams",
      "created_at" : "2009-08-18T18:34:31Z",
      "updated_at" : "2014-02-14T22:32:11Z"
    }
  }
]
```

### 获取快照(Get a shot)

```
GET /shots/:id
```

**图像**

`normal`的图像一般为400x300的，但如果是2012年10月4日之前创建的可能会更小一些。
`width`和`height`决定了`normal`图像的大小。

`hidpi`图像可能有也可能没有，但永远是800×600的。

`teaser`图像一般为200x150，但如果是2012年10月4日之前创建的可能会更小一些。

如果快照的`animated`属性存在(true)，快照中最高分辨率的图像（`hidpi`或`normal`）将被动态化（较小的图像将是静态的）。

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 471756,
  "title" : "Sasquatch",
  "description" : "<p>Quick, messy, five minute sketch of something that might become a fictional something.</p>",
  "width" : 400,
  "height" : 300,
  "images" : {
    "hidpi" : null,
    "normal" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch.png",
    "teaser" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch_teaser.png"
  },
  "views_count" : 4372,
  "likes_count" : 149,
  "comments_count" : 27,
  "attachments_count" : 0,
  "rebounds_count" : 2,
  "buckets_count" : 8,
  "created_at" : "2012-03-15T01:52:33Z",
  "updated_at" : "2012-03-15T02:12:57Z",
  "html_url" : "https://dribbble.com/shots/471756-Sasquatch",
  "attachments_url" : "https://api.dribbble.com/v1/shots/471756/attachments",
  "buckets_url" : "https://api.dribbble.com/v1/shots/471756/buckets",
  "comments_url" : "https://api.dribbble.com/v1/shots/471756/comments",
  "likes_url" : "https://api.dribbble.com/v1/shots/471756/likes",
  "projects_url" : "https://api.dribbble.com/v1/shots/471756/projects",
  "rebounds_url" : "https://api.dribbble.com/v1/shots/471756/rebounds",
  "animated" : false,
  "tags" : [
    "fiction",
    "sasquatch",
    "sketch",
    "wip"
  ],
  "user" : {
    "id" : 1,
    "name" : "Dan Cederholm",
    "username" : "simplebits",
    "html_url" : "https://dribbble.com/simplebits",
    "avatar_url" : "https://d13yacurqjgara.cloudfront.net/users/1/avatars/normal/dc.jpg?1371679243",
    "bio" : "Co-founder &amp; designer of <a href=\"https://dribbble.com/dribbble\">@Dribbble</a>. Principal of SimpleBits. Aspiring clawhammer banjoist.",
    "location" : "Salem, MA",
    "links" : {
      "web" : "http://simplebits.com",
      "twitter" : "https://twitter.com/simplebits"
    },
    "buckets_count" : 10,
    "comments_received_count" : 3395,
    "followers_count" : 29262,
    "followings_count" : 1728,
    "likes_count" : 34954,
    "likes_received_count" : 27568,
    "projects_count" : 8,
    "rebounds_received_count" : 504,
    "shots_count" : 214,
    "teams_count" : 1,
    "can_upload_shot" : true,
    "type" : "Player",
    "pro" : true,
    "buckets_url" : "https://dribbble.com/v1/users/1/buckets",
    "followers_url" : "https://dribbble.com/v1/users/1/followers",
    "following_url" : "https://dribbble.com/v1/users/1/following",
    "likes_url" : "https://dribbble.com/v1/users/1/likes",
    "shots_url" : "https://dribbble.com/v1/users/1/shots",
    "teams_url" : "https://dribbble.com/v1/users/1/teams",
    "created_at" : "2009-07-08T02:51:22Z",
    "updated_at" : "2014-02-22T17:10:33Z"
  },
  "team" : {
    "id" : 39,
    "name" : "Dribbble",
    "username" : "dribbble",
    "html_url" : "https://dribbble.com/dribbble",
    "avatar_url" : "https://d13yacurqjgara.cloudfront.net/users/39/avatars/normal/apple-flat-precomposed.png?1388527574",
    "bio" : "Show and tell for designers. This is Dribbble on Dribbble.",
    "location" : "Salem, MA",
    "links" : {
      "web" : "http://dribbble.com",
      "twitter" : "https://twitter.com/dribbble"
    },
    "buckets_count" : 1,
    "comments_received_count" : 2037,
    "followers_count" : 25011,
    "followings_count" : 6120,
    "likes_count" : 44,
    "likes_received_count" : 15811,
    "members_count" : 7,
    "projects_count" : 4,
    "rebounds_received_count" : 416,
    "shots_count" : 91,
    "can_upload_shot" : true,
    "type" : "Team",
    "pro" : false,
    "buckets_url" : "https://dribbble.com/v1/users/39/buckets",
    "followers_url" : "https://dribbble.com/v1/users/39/followers",
    "following_url" : "https://dribbble.com/v1/users/39/following",
    "likes_url" : "https://dribbble.com/v1/users/39/likes",
    "members_url" : "https://dribbble.com/v1/teams/39/members",
    "shots_url" : "https://dribbble.com/v1/users/39/shots",
    "team_shots_url" : "https://dribbble.com/v1/users/39/teams",
    "created_at" : "2009-08-18T18:34:31Z",
    "updated_at" : "2014-02-14T22:32:11Z"
  }
}
```

### 创建快照(Create a shot)

```
POST /shots
```

创建快照需要用户有`upload`域授权。被授权的用户也必须是一个玩家(player)或团队(teams)。

**参数**

参数名	|类型	|描述
----|----|----
title	|string	|**必须。** 快照的名字
image	|file	|**必须。** 图像的文件<br>它必须是400×300或800×600分辨率，不超过8M，必须是一个GIF，JPG或PNG。
description	|string	|快照的描述。
tags	|array	|快照的标签。<br/>最多可用有12个标签。
team_id	|integer	|与快照相关联的团队(team)的ID。<br/>被授权的用户必须是该团队(team)或该团队中的一员。
rebound_source_id	|integer	|An ID of a shot that the new shot is a rebound of.<sup>[不会翻译]( "被转发的快照的来源快照的ID。")</sup><br/>快照必须是可rebound的，且rebound的用户没有被认证用户屏蔽。


**响应**

Creating a shot happens asynchronously. After creation the returned location will return a 404 Not Found until processing is completed. If this takes longer than five minutes, be sure to contact support.

```
Status: 202 Accepted
Location: https://api.dribbble.com/v1/shots/471756
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
```

### 更新快照(Update a shot)

```
PUT /shots/:id
```

Updating a shot requires the user to be authenticated with the upload scope. The authenticated user must also own the shot.

**参数**

参数名	|类型	|描述
----|----|----
title	|string	|快照的标题。
description	|string	|快照的描述。
team_id	|integer	|与快照相关联的团队(team)的ID。<br/>The authenticated user must be on the team. If any empty value is provided the team association will be removed.
tags	|array	|快照的标签。<br/>Limited to a maximum of 12 tags. If any existing tags are not provided they will be removed.

**示例**

```
{
  "title" : "Sasquatch",
  "description" : "Quick, messy, five minute sketch of something that might become a fictional something.",
  "team_id" : 39,
  "tags" : [
    "fiction",
    "sasquatch",
    "sketch",
    "wip"
  ]
}
```

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 471756,
  "title" : "Sasquatch",
  "description" : "<p>Quick, messy, five minute sketch of something that might become a fictional something.</p>",
  "width" : 400,
  "height" : 300,
  "images" : {
    "hidpi" : null,
    "normal" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch.png",
    "teaser" : "https://d13yacurqjgara.cloudfront.net/users/1/screenshots/471756/sasquatch_teaser.png"
  },
  "views_count" : 4372,
  "likes_count" : 149,
  "comments_count" : 27,
  "attachments_count" : 0,
  "rebounds_count" : 2,
  "buckets_count" : 8,
  "created_at" : "2012-03-15T01:52:33Z",
  "updated_at" : "2012-03-15T02:12:57Z",
  "html_url" : "https://dribbble.com/shots/471756-Sasquatch",
  "attachments_url" : "https://api.dribbble.com/v1/shots/471756/attachments",
  "buckets_url" : "https://api.dribbble.com/v1/shots/471756/buckets",
  "comments_url" : "https://api.dribbble.com/v1/shots/471756/comments",
  "likes_url" : "https://api.dribbble.com/v1/shots/471756/likes",
  "projects_url" : "https://api.dribbble.com/v1/shots/471756/projects",
  "rebounds_url" : "https://api.dribbble.com/v1/shots/471756/rebounds",
  "animated" : false,
  "tags" : [
    "fiction",
    "sasquatch",
    "sketch",
    "wip"
  ],
  "team" : {
    "id" : 39,
    "name" : "Dribbble",
    "username" : "dribbble",
    "html_url" : "https://dribbble.com/dribbble",
    "avatar_url" : "https://d13yacurqjgara.cloudfront.net/users/39/avatars/normal/apple-flat-precomposed.png?1388527574",
    "bio" : "Show and tell for designers. This is Dribbble on Dribbble.",
    "location" : "Salem, MA",
    "links" : {
      "web" : "http://dribbble.com",
      "twitter" : "https://twitter.com/dribbble"
    },
    "buckets_count" : 1,
    "comments_received_count" : 2037,
    "followers_count" : 25011,
    "followings_count" : 6120,
    "likes_count" : 44,
    "likes_received_count" : 15811,
    "members_count" : 7,
    "projects_count" : 4,
    "rebounds_received_count" : 416,
    "shots_count" : 91,
    "can_upload_shot" : true,
    "type" : "Team",
    "pro" : false,
    "buckets_url" : "https://dribbble.com/v1/users/39/buckets",
    "followers_url" : "https://dribbble.com/v1/users/39/followers",
    "following_url" : "https://dribbble.com/v1/users/39/following",
    "likes_url" : "https://dribbble.com/v1/users/39/likes",
    "members_url" : "https://dribbble.com/v1/teams/39/members",
    "shots_url" : "https://dribbble.com/v1/users/39/shots",
    "team_shots_url" : "https://dribbble.com/v1/users/39/teams",
    "created_at" : "2009-08-18T18:34:31Z",
    "updated_at" : "2014-02-14T22:32:11Z"
  }
}
```

### 删除快照(Delete a shot)

```
DELETE /shots/:id
```

删除快照需要用户拥有`upload`域授权。被授权用户同时必须是该快照的拥有者。
Deleting a shot requires the user to be authenticated with the upload scope. The authenticated user must also own the shot.