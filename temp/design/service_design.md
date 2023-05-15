# Service Design

设计模板如下，具体设计思路应更新在《设计文档》中，有些参数设计仍需商榷：

| 方法签名 | 描述 |
| -------- | ---- |
|          |      |

## UserService

| 方法签名                                                     | 描述                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| public String authenticateUser(VerifyUserLoginRequest verifyUserLoginRequest) throws UserException; | 验证用户输入的用户名和密码，并生成token     |
| public String authenticateAdmin(VerifyAdminLoginRequest verifyAdminLoginRequest) throws UserException; | 验证管理员输入的用户名和密码，并生成token   |
| public int getUserIdFromToken(String token) throws UserException; | 验证提供的token是否有效，并返回相应的UserId |
| public boolean addUser(VerifyUserRegisterRequest verifyUserRegisterRequest) throws UserException; | 创建新的用户                                |
| public User getUser(String userId) throws UserException;     | 获取用户信息                                |
| public string getPassword(GetPasswordRequest getPasswordRequest) throws UserException; | 获取用户的密码                              |
| public boolean updatePassword(UpdatePasswordRequest updatePasswordRequest) throws UserException; | 修改用户密码                                |
| public List<User> getUserList(GetAccountInfoListRequest getAccountInfoListRequest) throws UserException; | 获取用户列表                                |
| public boolean updateUser(UpdateAccountInfoRequest updateAccountInfoRequest) throws UserException; | 更新用户信息                                |
| public boolean deleteUser(DeleteAccountRequest deleteAccountRequest) throws UserException; | 删除用户                                    |
| public List<UserSummary> getUserSummary() throws UserException; | 获取用户总体统计数据                        |

## LogService

| 方法签名                                                     | 描述                     |
| ------------------------------------------------------------ | ------------------------ |
| public void addLog(int curUserId) throws LogException;       | 添加一条新的登陆记录     |
| public void deleteLog(Date date) throws LogException;        | 删除某个日期之前所有记录 |
| public List<LogSummary> getLogSummary() throws LogException; | 获取登录总体统计数据     |

## PostService

| 方法签名                                                     | 描述                 |
| ------------------------------------------------------------ | -------------------- |
| public List<Post> getPostList(ListPostRequest listPostRequest) throws PostException; | 按页获取帖子列表     |
| public boolean addPost(AddPostRequest addPostRequest) throws PostException; | 添加新帖子           |
| public boolean deletePost(DeletePostRequest deletePostRequest) throws PostException; | 删除帖子             |
| public Post getPost(string postId) throws PostException;     | 获取帖子详细信息     |
| public List<PostSummary> getPostSummary() throws PostException; | 获取帖子总体统计数据 |

## LikeService

| 方法签名                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public boolean  addLike(String userId, String postId) throws LikeException; | 用户点赞时，添加新的点赞关系                                 |
| public boolean  deleteLike(String userId, String postId) throws LikeException; | 用户取消点赞时，删除点赞关系                                 |
| public boolean  getLikeNum(int postId) throws LikeException; | 获取对应帖子点赞数目                                         |
| public boolean getLiked(int curUserId, int postId) throws LikeException; | 获取相应用户对相应帖子的是否点赞，用于帖子显示，扣除积分，点赞/取消时的检查 |
| public List<LikeSummary> getLikeSummary() throws LikeException; | 获取点赞总体统计数据                                         |

## CommentService

删除帖子时使用级联删除的方式删除评论。

| 方法签名                                                     | 描述                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| public boolean addComment(CommentPostRequest commentPostRequest) throws CommentException; | 添加新的评论                           |
| public boolean deleteComment(DeletCommentRequest deletCommentRequest, int curUserId) throws CommentException; | 删除某条评论，注意检查评论是否属于用户 |
| public List<Comment> getCommentList(int postId) throws CommentException; | 获取对应帖子在相对位置的几条评论       |
| public boolean deleteCommentAll(int postId) throws CommentException; | 删除对应帖子的全部评论，用于评论删除   |
| public List<CommentSummary> getCommentSummary() throws CommentException; | 获取评论总体统计数据                   |

## ReplyService

删除帖子或评论时使用级联删除删除相应回复。

| 方法签名                                                     | 描述                                               |
| ------------------------------------------------------------ | -------------------------------------------------- |
| public boolean addReply(ReplyCommentRequest replyCommentRequest) throws ReplyException; | 添加新的回复                                       |
| public boolean deleteReply(DeletCommentRequest deletCommentRequest) throws ReplyException; | 删除相应的回复                                     |
| public List<Reply> getReplyList(int postId, int commentId) throws ReplyException; | 获取对应帖子对应评论的前几条回复                   |
| public List<Reply> getReplyAll(int postId, int commentId) throws ReplyException; | 获取对应帖子对应评论的全部回复                     |
| public boolean deleteReplyAll(int postId) throws ReplyException; | 删除对应帖子对应评论的全部回复，用于帖子删除       |
| public boolean deleteReplyAll(int postId, int commentId) throws ReplyException; | @重载 删除对应帖子对应评论的全部回复，用于评论删除 |
| public List<ReplySummary> getReplySummary() throws ReplyException; | 获取回复总体统计数据                               |

## RecourseService

| 方法签名                                                     | 描述                 |
| ------------------------------------------------------------ | -------------------- |
| public List<Resource> getResourceRecommended(ListRecommendResoueceRequest listRecommendResoueceRequest) throws ResourceException; | 获取推荐资源列表     |
| public List<Resource> getResourceByCategory(ListResourceByCategoryRequest listResourceByCategoryRequest) throws ResourceException; | 按类搜索资源         |
| public boolean addResource(UploadResourceRequest uploadResourceRequest) throws ResourceException; | 添加新资源           |
| public boolean deleteResource(DeleteResourceRequest deleteResourceRequest) throws ResourceException; | 删除资源             |
| public boolean getResourceUrl(DownloadResourceRequest downloadResourceRequest) throws ResourceException;<br />这个咋实现啊？ | 下载资源             |
| public Resource getResourceDetailed(String resourceId) throws ResourceException; | 获取资源详情         |
| public List<ResourceSummary> getResourceSummary() throws ResourceException; | 获取资源总体统计数据 |
| public List<ResourceSummary> getResourceSummaryByCategory() throws ResourceException; | 获取资源按类统计数据 |

## DownloadHistoryService

| 方法签名                                                     | 描述                     |
| ------------------------------------------------------------ | ------------------------ |
| public List<DownloadHistory> getDownloadHistory(GetDownloadHistoryRequest getDownloadHistoryRequest) throws DownloadHistoryException; | 按页获取下载历史         |
| public boolean deleteDownloadHistory(String resourceId) throws DownloadHistoryException; | 清空某资源下载历史       |
| public List<DownloadHistorySummary> getDownloadHistorySummary() throws DownloadHistoryException; | 获取下载历史相关统计数据 |

## StatisticsService

| 方法签名                                                     | 描述                             |
| ------------------------------------------------------------ | -------------------------------- |
| public List<StatisticsSummary> getOverallInfo(HttpServletRequest request) throws StatisticsException; | 获取总体信息                     |
| public int getNumOfCurrentOnline(HttpServletRequest request) throws StatisticsException; | 获取当前在线                     |
| public List<PostSummary> getPostListOrderedByPopularity(TimeRange timeRange, HttpServletRequest request) throws StatisticsException; | 根据热度对帖子排序并获取         |
| public List<ResourceSummary> getResourceListByDownload(TimeRange timeRange, HttpServletRequest request) throws StatisticsException; | 根据下载量对资源排序并获取       |
| public List<UserSummary> getUserListByCntOfResourceUpload(TimeRange timeRange, HttpServletRequest request) throws StatisticsException; | 根据上传资源数量对用户排序并获取 |

## ExperienceService

| 方法签名                                                     | 描述                               |
| ------------------------------------------------------------ | ---------------------------------- |
| public boolean updateExperience(int curUserId, int changeNumber) throws ExperienceException; | 为相应用户增加/扣除积分            |
| public int getExperience2Level(int curUserId) throws ExperienceException; | 获取相应用户的等级                 |
| public boolean getExperienceForPost(int curUserId, int postId) throws ExperienceException; | 检查相应用户是否有权查看某帖子内容 |