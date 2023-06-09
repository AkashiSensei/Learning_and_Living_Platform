# 软工大作业的一些笔记

## 时间节点

第9周：《软件开发计划书》《需求规格说明书》

第12周：《软件设计说明书》

第15周：《源代码》《可执行程序》《测试报告》《部署文档》《用户使用说明书》，现场展示

**推送之前先拉取**

## TODO LIST

### 修改已经提交过的部分

- [ ] 修改用例的网页跳转部分，我们计划让访客、用户、管理员的默认页面都是教育资源相关页面。
- [x] 修改用例的管理员用户删除部分，计划添加批量删除功能，如果之前没有的话。
- [ ] 帖子删除等等不再异步进行了。

### 对当且阶段已有的设计进行小改动

- [x] 将图片的保存方式变为各个表存储url，因此应该不再需要image表了。
- [x] 同理，资源路径是不是也应该改为资源url？不过这个我不是很懂，应该是提供一个url然后建立连接来下载吧。
- [x] 为Post类添加缩略图url列表，相当于两个url列表，一个存缩略图路径，另外一个存原图路径。
- [x] 在User表里面维护一下登陆天数好了。
- [x] 管理员只需要id、密码和邮箱就行了吧，管理员是不是不能修改自己的个人信息。
- [x] 用户和管理员的password不够长吧，这里应该保存的是加密加盐之后的密文吧。
- [x] 暂时打算加上删除日志（某某日期之前）和清空下载历史的功能，涉及对用例的修改以及对Mapper的修改。
- [x] 给点赞也加上对时间的记录吧，能记录多长时间内有多少点赞。
- [x] 在之后设计完成的基础上对 Mapper 和数据库等等进行相应的修改。

### 主要设计

- [x] 设计各种Service类，作为之后的基础，目前的Service大概分为两层，上层的包括Post和Resource之类的，下层的包括User和权限之类的。
- [x] 完善请求相关的实体类，即各种Request类，有哪些Request类应该在Service中已经指明了，因此这步应该只用完善，明确其中需要包含哪些属性，即有哪些信息需要传送到后端，可以参考方方和陈哥的接口设计。
- [x] 实体类设计，增加PostSummary和PostDetail等实体类作为请求的返回，这两个中注意添加当前用户是否有资格删除的属性。这部分应该不太多，可以和上一个一起完成。
- [x] 异常类设计。
- [x] 完善各种Controller类，基本上和Service是对应的，大概只需要改一下返回值和参数等等，设计一下绑定到的目标url，请求的类型等等，也可以参考方方和陈哥的接口设计。注意对管理员和用户共享的一些功能的处理方式。
- [ ] 将已经设计出来的各个类分到组件和子系统，为之后的画图做准备。别忘了咱自己要写的 RestBean类和拦截器。

### 画图

设计完成之后进行画图，现在先不急，问题不大，加油加油。

### 其它

- [x] 修改一下temp目录的结构，并统一一下各种文件的命名

## 任务说明

### 2023/5/13洲洲洲

> 这部分中进行的设计已经做出修改。

用了很久的时间解决设计过程中的各种各样的问题，并找出了一个比较合理的架构，大家只需要按照这个架构完成设计就行。但是切记切记一定要在设计的过程中多思考思考，上述设计的任务都不是文字性的任务，在设计的过程中一定要想一想自己写下来的东西是不是合理的，想一想我写的东西是不是合理的，转化成代码的时候会不会遇到问题，代码能不能跑通等等各种各样的问题。然后就是需要大家能够独当一面，完成发现问题，分析问题到提出合理的解决方案的整个流程，不要仅仅仿照网上的思路，一定要多思考思考结合咱自己的项目，最终目的是不要在自己的设计中留下问题，让别人来解决。遇到自己不太清楚的地方，一定去了解学习一下，千万别就按照已经提出来的设计思路不动脑子往下走。谢谢大家，给各位磕一个。这两天在后端设计的过程中一直走不下去一直发现各种问题，然后都要自己设计，从顶到底全要完整的装到我的脑子里，很折磨。

目前整体的后端设计思路大概是，发过来的请求包含token，由拦截器处理token转化成userId放在HttpServletRequest中。然后各个Controller方法中提取HttpServletRequest中的userId，和传给Controller方法的咱自己设计的各个Request类一起传给Service方法。Service方法可以调用别的Service方法，基本上是上层的Service调用下层的Service，Service和Mapper基本对应。Service返回相应的数据或者状态，比如包含数据的List<PostSummary>，或者表示成功或错误原因的int值，由Controller方法进行处理和包装，最后返回 RestBean类。

一定要理解整体的设计在写自己的部分，多思考思考，谢谢大家了，另外可以看一下目前temp目录里面已经有的文件，理解一下，有啥问题问小chai+搜索+问，但是也不要太相信小chai（）。

时间真的非常非常紧，仅仅软工一门课，后面就还有开发、实现说明文档、测试、测试说明文档、部署、部署说明等等非常多东西，每个人必须都要认真的搞软工了，搞得时候真不能想着赶紧把软工搞完做自己别的作业，由纰漏的地方最后全都会丢给别人和即将期末考试的自己。再给各位磕一个。

TODO LIST各位发现问题随时修改/补充，设计整体设计的改动记得在群里说一声。

再给各位磕一个，真得靠每个人努力。
