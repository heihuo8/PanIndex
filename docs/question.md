## 常见问题

### 如何获取目录ID？
正常访问官方网盘页面，进入到你想分享目录的页面，浏览器里地址栏最后面的就是目录ID

若要使用teambition项目版：rootId，请使用**项目id**

![image-20210312180742254](_images/teambition-project.png)

**注**：当网盘启用本地模式，目录ID为分享目录的绝对路径，比如我想分享本地的`/opt`目录，`root_id`为`/opt`，密码目录同理

### PanIndex为何不使用前后端分离？
PanIndex的设计初衷是简单高效，前后分离会增加部署的复杂度，且会增加页面响应时间，PanIndex为单页面应用，目前页面的管理也相对容易，也为了更方便的适配heroku，目前将html，js，css，image都打包到二进制文件中，所以通常你只需要一个二进制文件加一个配置文件即可。
～～PanIndex依然可以作为纯后端使用，可以根据开放接口，开发自己的前端主题～

### 如何自定义页面？
参考[自定义主题](/#自定义主题)

### 登录失效、目录不更新该如何解决？
程序启动时会初始化登录状态。按照配置执行定时任务，默认登录cookie刷新天执行一次，经测试天翼云，teambition的cookie都比较稳定，所以cookie刷新也不建议频繁执行，频繁执行会导致验证登录。

计划任务修改配置中cron表达式，[cron在线生成](https://cron.qqe2.com/)

如果你更新了网盘文件想要立刻生效，可以手动刷新目录缓存

## 网盘目录空白

由于PanIndex使用了SQLite来做数据存储，Heroku会定期清理本地文件，请每天至少执行一次同步缓存的任务，时间可以设置为cookie刷新之后，且尽量选择闲时来同步

### 天翼云出现验证码登录，如何解决？
2.x关闭了打码狗的使用，若出现验证登录，请等一小时后再尝试。
开发调试：注释掉程序启动刷新COOKIE的代码

### 网盘使用经验

1. 天翼云网盘：普通版容量较小，15G空间，如果文件被多个不同ip访问下载，有一定几率触发限速，会员也无法幸免。
2. teambition-项目文件：个人测试速度限制在500K左右，不过容量暂时没有限制，也不需要内测资格即可使用。
3. teambition-个人文件：无限速，有使用空间限制，目前有2T空间，后期可能会合并到阿里云盘，不清楚会不会一直存在。
4. 本地目录：下载会占用服务器的带宽，而且服务器到期可能要面临文件的转移。
5. 阿里云盘：内测+teambition合并有3T，公测使用各种福利码可以达到8T，不过空间可能会回收，不确定是不是永久，阿里云一直都很套路，你懂得，据网友反馈，使用目录程序分享账号可能会ban，管控上比teambition更严格。