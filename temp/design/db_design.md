# 数据库设计：

| 表名               | 描述         | 主键 | 索引                             | 触发器              |
| ------------------ | ------------ | ---- | -------------------------------- | ------------------- |
| User               | 用户信息     | id   |                                  | user_insert_trigger |
| UserOnline         | 在线用户信息 | id   |                                  |                     |
| Admin              | 管理员信息   | id   |                                  |                     |
| Post               | 帖子         | id   | userId                           |                     |
| Like               | 点赞         | id   | postId,userId                    |                     |
| Comment            | 评论         | id   | postId,userId                    |                     |
| Reply              | 评论的回复   | id   | commentId,postId,userId          |                     |
| Resource           | 教育资源     | id   | userId,(title,content)           |                     |
| Log                | 登录日志     | id   | userId                           |                     |
| DownloadHistory    | 下载记录     | id   | resourceId，downloadTime，userId |                     |
| ResourceCategories | 教育资源类别 | id   | resourceId,category              |                     |

## User表

| 字段名         | 类型        | 约束         | 备注         |
| -------------- | ----------- | ------------ | ------------ |
| id             | int         | 主键，自增   |              |
| name           | varchar(20) |              | 最长20字符   |
| password       | varchar(255) |              | 加盐加密密码 |
| email          | varchar(40) |              | 邮箱         |
| gender         | enum        |              | 性别         |
| birthday       | Date        |              | 生日         |
| salt           | varchar(20) |              | 加密盐值     |
| registerTime   | Date        |              | 注册时间     |
| profilePhotoUrl | varchar(255)         |  | 头像         |
| LogInNum | int | | 登陆天数 |

## UserOnline

| 字段名          | 类型         | 约束       | 备注         |
| --------------- | ------------ | ---------- | ------------ |
| id              | int          | 主键，自增 |              |
| name            | varchar(20)  |            | 最长20字符   |
| password        | varchar(255) |            | 加盐加密密码 |
| email           | varchar(40)  |            | 邮箱         |
| gender          | enum         |            | 性别         |
| birthday        | Date         |            | 生日         |
| salt            | varchar(20)  |            | 加密盐值     |
| registerTime    | Date         |            | 注册时间     |
| profilePhotoUrl | varchar(255) |            | 头像         |
| LogInNum        | int          |            | 登陆天数     |
| token           | varchar(255) |            | 用户token    |

## Admin表

| 字段名         | 类型        | 约束         | 备注         |
| -------------- | ----------- | ------------ | ------------ |
| id             | int         | 主键，自增   |              |
| password       | varchar(255) |              | 加盐加密密码 |
| email          | varchar(40) |              | 邮箱         |
| salt           | varchar(20) |              | 加密盐值     |

## Post表

| 字段名            | 类型        | 约束        | 备注               |
| ----------------- | ----------- | ----------- | ------------------ |
| id                | int         | 主键，自增  |                    |
| title             | varchar(30) |             | 帖子标题，最多30字 |
| userId         | int         | 外键User.id ON DELETE SET NULL | 发布者id           |
| content           | text        |             | 帖子内容           |
| floorCount      | int         |             | 楼层数             |
| postTime         | Datetime    |             | 发布时间           |
| thumbnail1,thumbnail2,... | varchar(2048)     |  | 拥有的缩略图们         |
| imageUrl,imageUrl,... | varchar(2048)     |  | 拥有的图片们         |
| likeCount  | int         |             | 点赞数             |
| authority | int | | 帖子权限 |
| browseCount | int | | 浏览数 |
| updateTime | datetime | | 更新时间 |

## Like

| 字段名   | 类型     | 约束                  | 备注     |
| -------- | -------- | --------------------- | -------- |
| id       | int      | 主键，自增            |          |
| postId   | int      | 外键Post.id，级联删除 | 所属帖子 |
| userId   | int      | 外键User.id           | 所属用户 |
| likeTime | Datetime |                       | 点赞时间 |

## Comment

| 字段名      | 类型         | 约束                            | 备注                   |
| ----------- | ------------ | ------------------------------- | ---------------------- |
| id          | int          | 主键，自增                      |                        |
| postId      | int          | 外键，Post.id，级联删除         | 所属帖子id             |
| userId      | int          | 外键User.id，ON DELETE SET NULL | 发布者id               |
| publishTime | Datetime     |                                 | 评论时间               |
| content     | varchar(255) |                                 | 评论内容,最多255字     |
| imageUrl     | varchar(255)          |                | 评论图片，限定至多一张 |
| floor       | int          |                                 | 第几楼                 |

## Reply

| 字段名      | 类型         | 约束                           | 备注                |
| ----------- | ------------ | ------------------------------ | ------------------- |
| id          | int          | 主键，自增                     |                     |
| postId      | int          | 外键，Post.id，级联删除        | 所属帖子id          |
| commentId   | int          | 外键，Comment.id，级联删除     | 所属评论id          |
| userId      | int          | 外键User.id ON DELETE SET NULL | 回复者id            |
| publishTime | datetime     |                                | 回复时间，精确到秒  |
| content     | varchar(255) |                                | 回复内容，最多255字 |

## Resource

| 字段名        | 类型     | 约束                           | 备注               |
| ------------- | -------- | ------------------------------ | ------------------ |
| id            | int      | 主键，自增                     |                    |
| userId        | int      | 外键User.id ON DELETE SET NULL | 发布者id           |
| title | varchar(30) |  | 资源标题 |
| subject       | enum     |                                | 资源学科           |
| category      | enum     |                                | 资源类型           |
| publishedTime | Datetime |                                | 发布时间，精确到秒 |
| size          | int      |                                | 大小               |
| content       | text     |                                | 资源简介           |
| path          | char     |                                | 资源路径           |
| imageUrl       | varchar(255)    |                    | 资源封面           |
| downloadCount | int      |                                | 下载量             |
| authority     | int      |                                | 权限               |
| downloadUrl | varchar(255) | | 下载链接 |

## Log

| 字段名     | 类型     | 约束                           | 备注               |
| ---------- | -------- | ------------------------------ | ------------------ |
| id         | int      | 主键，自增                     |                    |
| userId     | int      | 外键User.id ON DELETE SET NULL | 登陆者id           |
| loginTime  | Datetime |                                | 登陆时间，精确到秒 |
| logoutTime | Datetime |                                | 登出时间，精确到秒 |



## DownloadHistory

| 字段名       | 类型         | 约束                           | 备注               |
| ------------ | ------------ | ------------------------------ | ------------------ |
| id           | int          | 主键，自增                     |                    |
| userId       | int          | 外键User.id ON DELETE SET NULL | 下载者id           |
| resourceId   | int          | 外键Resource.id                | 资源id             |
| title        | varchar(30)  |                                | 资源标题           |
| downloadTime | Datetime     |                                | 下载时间，精确到秒 |
| fileName     | varchar(255) |                                | 资源文件名         |

---

MAKIMA：热度的定义和实现？

——生姜烧肉

---

## Experience

| 字段名   | 类型 | 约束                            | 备注     |
| -------- | ---- | ------------------------------- | -------- |
| id       | int  | 外键User.id，ON DELETE SET NULL | 用户id   |
| exp      | int  |                                 | 经验     |
| dailyEXP | int  |                                 | 每日经验 |

## ResourceCategories

| 字段名     | 类型 | 约束              | 备注     |
| ---------- | ---- | ----------------- | -------- |
| id         | int  | 主键自增          |          |
| resourceId | int  | 外键，Resource.id | 资源id   |
| category   | int  |                   | 资源类别 |
