```
（用户） 1、
（系统） 2、


（） a、
	（用户） 1、
	（系统） 2、
（） a、
	（用户） 1、
	（系统） 2、
（） a、
	（用户） 1、
	（系统） 2、



1、
```

```
（用户） 1、管理员点击“查看统计数据”按钮。
（系统） 2、跳转至查看统计数据页面，展示统计数据。


（可选） a、管理员可以查看不同的统计数据
	（用户） 1、管理员点击想要查看的统计数据类别，或对参与统计的数据进行筛选。
	（系统） 2、系统根据管理员的选择展示相应的数据。
（） a、
	（用户） 1、
	（系统） 2、
（） a、
	（用户） 1、
	（系统） 2、



1、应保证页面加载速度。
```

| 用例名称       |      |
| -------------- | ---- |
| **用例编号**   |      |
| **参与者**     |      |
| **用例描述**   |      |
| **触发器**     |      |
| **前置条件**   |      |
| **后置条件**   |      |
| **基本事件流** |      |
| **扩展事件流** |      |
| **补充约束**   |      |

| 用例名称       | 修改个人信息                                                 |
| -------------- | ------------------------------------------------------------ |
| **用例编号**   | UC011                                                        |
| **参与者**     | 用户                                                         |
| **用例描述**   | 用户在个人信息界面修改个人信息                               |
| **触发器**     | 用户点击个人信息界面中的“编辑个人信息”按钮                   |
| **前置条件**   | 系统处于登陆状态，当前页面为个人信息页面                     |
| **后置条件**   | 系统中保存到用户信息依照用户的想法得到更新，仍处于个人信息页面 |
| **基本事件流** | （用户） 1、用户在个人信息界面点击“编辑个人信息”按钮<br/>（系统） 2、系统将个人简介等允许修改的个人信息的显示方式修改为文本框，使用户能够编辑其内容。<br/>（用户） 3、用户编辑文本框中的内容，并点击“保存”按钮提交修改。<br/>（系统） 4、弹出提示框告知用户修改成功，并依照用户输入更新相应账户数据，取消文本框的显示方式，正常展示修改完的信息。 |
| **扩展事件流** | （可选） 3a、用户可以取消修改个人信息<br/>	（用户） 1、用户点击“取消”按钮。<br/>	（系统） 2、系统取消文本框的显示方式，丢弃修改，正常展示修改前的信息，中止修改个人信息。<br />（异常处理） 3b、用户非法输入<br/>	（用户） 1、用户输入超长内容或输入非法字符。<br />	（系统） 2、系统检测到用户的非法输入，及时在输入框旁边对用户进行提示，并使“保存”按钮无效。<br />	（用户） 3、用户修改输入直至合法。<br/>	（系统） 4、系统关闭非法提示，使能“保存”按钮。 |
| **补充约束**   | 无                                                           |

