# Dribbble API 文档
* [图集(Buckets)](#图集buckets)
* [快照(Shots)](#快照shots)

## 图集(Buckets)

> 扩展阅读: [Buckets are collections of shots](https://dribbble.com/buckets)

* [图集(Buckets)](#图集buckets)
  * [获取图集(Get a bucket)](#获取一个图集get-a-bucket)
  * [创建图集((Create a bucket))](#创建一个图集create-a-bucket)
  * [更新图集(Update a bucket)](#更新图集update-a-bucket)
  * [删除图集(Delete a bucket)](#删除图集delete-a-bucket)
  * [图集快照(Shots)](#图集快照shots)
* [工程(Project)](#工程project)

### 获取图集(Get a bucket)

```
GET /buckets/:id
```

> 扩展范例: `https://dribbble.com/simplebits/buckets/2754` （下方响应中的报文）    
> 参见： [https://dribbble.com/simplebits/buckets/2754](https://dribbble.com/simplebits/buckets/2754)

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 2754,
  "name" : "Great Marks",
  "description" : "Collecting superb brand marks from the <a href=\"https://dribbble.com\">Dribbbleverse</a>.",
  "shots_count" : 251,
  "created_at" : "2011-05-20T21:05:55Z",
  "updated_at" : "2014-02-21T16:37:12Z",
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
  }
}
```

### 创建图集(Create a bucket)

```
POST /buckets
```

创建图集需要具有写入域权限的认证用户。该用户同时必须是图集的拥有者。

**参数**

Name	|Type	|Description
----|----|----
name	|string	|**必须**。 图集的名称。
description	|string	|图集的描述。


**范例**

```
{
  "name" : "Great Marks",
  "description" : "Collecting superb brand marks from the <a href=\"https://dribbble.com\">Dribbbleverse</a>."
}
```

**响应**

```
Status: 201 Created
Location: https://api.dribbble.com/v1/buckets/2754
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 2754,
  "name" : "Great Marks",
  "description" : "Collecting superb brand marks from the <a href=\"https://dribbble.com\">Dribbbleverse</a>.",
  "shots_count" : 251,
  "created_at" : "2011-05-20T21:05:55Z",
  "updated_at" : "2014-02-21T16:37:12Z"
}
```

###更新图集(Update a bucket)

```
PUT /buckets/:id
```

更新图集需要具有写入域权限的认证用户。该用户同时必须是图集的拥有者。

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 2754,
  "name" : "Great Marks",
  "description" : "Collecting superb brand marks from the <a href=\"https://dribbble.com\">Dribbbleverse</a>.",
  "shots_count" : 251,
  "created_at" : "2011-05-20T21:05:55Z",
  "updated_at" : "2014-02-21T16:37:12Z"
}
```

###删除图集(Delete a bucket)

```
DELETE /buckets/:id
```

删除图集需要具有写入域权限的认证用户。该用户同时必须是图集的拥有者。

**响应**

```
Status: 204 No Content
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
```



## 图集快照(Shots)

* [图集(Buckets)](#图集buckets)
  * [获取图集(Get a bucket)](#获取一个图集get-a-bucket)
  * [创建图集((Create a bucket))](#创建一个图集create-a-bucket)
  * [更新图集(Update a bucket)](#更新图集update-a-bucket)
  * [删除图集(Delete a bucket)](#删除图集delete-a-bucket)
  * [图集快照(Shots)](#图集快照shots)
    * [列出图集中的快照(List shots for a bucket)](#列出图集中的快照list-shots-for-a-bucket)
    * [向图集中添加快照(Add a shot to a bucket)](#向图集中添加快照add-a-shot-to-a-bucket)
    * [从图集中删除快照(Remove a shot from a bucket)](#从图集中删除快照remove–a-shot-from–a–bucket)
* [工程(Project)](#工程project)

###列出图集中的快照(List shots for a bucket)

```
GET /buckets/:id/shots
```

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

###向图集中添加快照(Add a shot to a bucket)

```
PUT /buckets/:id/shots
```

向图集中添加快照需要具有写入域权限的认证用户。该用户同时必须是图集的拥有者。

**参数**

Name	|Type	|Description
----|----|----
shot_id	|integer	|要添加的快照id。

**响应**

```
Status: 204 No Content
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
```

###从图集中删除快照(Remove a shot from a bucket)

```
DELETE /buckets/:id/shots
```

从图集中删除快照需要具有写入域权限的认证用户。该用户同时必须是图集的拥有者。

**参数**

Name	|Type	|Description
----|----|----
shot_id	|integer	|要删除的快照id。

**响应**

```
Status: 204 No Content
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
```



## 工程(Project)

* [图集(Buckets)](#图集buckets)
* [工程(Project)](#工程project)
  * [获取一个工程(Get a project)](#获取一个工程get-a-project)
  * [工程快照(Shots)](#工程快照shots)

###获取一个工程(Get a project)

```
GET /projects/:id
```

**响应**

```
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
{
  "id" : 3,
  "name" : "Web Standards Sherpa",
  "description" : "I did visual design and art direction for this project, working with the <a href=\"http://webstandards.org\">Web Standards Project</a> and Microsoft.",
  "shots_count" : 4,
  "created_at" : "2011-04-14T03:43:47Z",
  "updated_at" : "2012-04-04T22:39:53Z",
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
  }
}
```

##工程快照(Shots)
* [图集(Buckets)](#图集buckets)
* [工程(Project)](#工程project)
  * [获取一个工程(Get a project)](#获取一个工程get-a-project)
  * [工程快照(Shots)](#工程快照shots)
    * [列出工程中的快照(List shots for a project)](#列出工程中的快照list-shots-for-a-project))

###列出工程中的快照(List shots for a project)

```
GET /projects/:id/shots
```

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